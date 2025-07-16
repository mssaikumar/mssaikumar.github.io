Thanks! I’ll prepare a comprehensive guide for migrating from Quartz Scheduler 2.1.6 to 2.3.2 using Java Zulu 8 and Spring Framework 5.3.31, assuming a single-node deployment. I’ll also include considerations for JDBC and RAM job stores, and note what to look for if custom jobs or Spring integration are present.

I’ll let you know when everything is ready.


# Migrating Quartz Scheduler 2.1.6 to 2.3.2

## 1. Update Dependencies in Your Build

Begin by updating your project’s dependencies to use Quartz **2.3.2**. In Maven, that means changing the Quartz scheduler dependency version to 2.3.2 in your `pom.xml`. For example:

```xml
<dependency>
    <groupId>org.quartz-scheduler</groupId>
    <artifactId>quartz</artifactId>
    <version>2.3.2</version>
</dependency>
```

If your project previously used a **`quartz-all`** JAR or separate Quartz modules (like `quartz-jobs`), be aware that by Quartz 2.3.x you may need to include the core Quartz artifact (as above) and any additional modules individually. For instance, if you use any of Quartz’s built-in jobs or plugins that were in a separate JAR, ensure those are added (Quartz 2.3.2’s main artifact generally includes core functionality).

Also update any **Spring-related Quartz integration** libraries if present:

* If you see a dependency like `spring-integration-quartz` (part of Spring Integration), make sure it’s a version compatible with Spring 5.3.x. Spring Integration 5.x supports Quartz 2.x, so it should work with 2.3.2. No code changes are usually needed for Spring’s Quartz integration classes when updating the Quartz version – Spring’s `SchedulerFactoryBean` and related classes in Spring 5.3 already support Quartz 2.x. Just ensure the Quartz 2.3.2 library is on the classpath so Spring can use it.
* If you *aren’t actually using* the Spring Integration Quartz features, having that dependency won’t affect the migration, but you might consider removing it to reduce complexity.

Quartz 2.3.2 requires **Java 7 or higher**, which is satisfied by your Java 8 (Zulu 8) environment. Spring Framework 5.3.31 is fully compatible with Quartz 2.3.x as well, so you don’t need to upgrade Spring itself for this Quartz update.

After updating the Maven POM and pulling in Quartz 2.3.2, rebuild the project. This will surface any compilation issues due to API changes (addressed below).

## 2. Verify Single-Node vs Clustered Configuration

You mentioned the application runs in “single node mode.” In Quartz terms, this likely means clustering is **not** enabled. Quartz can run in a clustered mode (multiple scheduler instances coordinating through the database) or as a single instance. It’s important to confirm this, because it affects configuration and the database setup:

* **Check your Quartz properties** (often in a `quartz.properties` file or set via Spring): look for the setting `org.quartz.jobStore.isClustered`. If it’s `false` or not present, the scheduler is not in clustered mode (single-node setup). If it’s `true`, then Quartz is configured for clustering. In single-node deployments, clustering is typically turned off.
* Also check `org.quartz.jobStore.class` to see what JobStore is in use. For a JDBC-backed store it will be something like `org.quartz.impl.jdbcjobstore.JobStoreTX` or `JobStoreCMT`. If instead you see `org.quartz.simpl.RAMJobStore`, then the scheduler is not using a database at all (pure in-memory). Given that you mention a schema, it’s likely using a JDBC JobStore.

For a **single-node, JDBC JobStore** (non-clustered) setup, you can leave `isClustered=false`. Quartz will use the database just for persistence (so jobs/triggers survive restarts or crashes), but it won’t acquire DB locks for clustering. If by chance `isClustered` was set to true in your config even though you run only one instance, it won’t harm functionality – but it will impose some overhead. You could disable it for simplicity. In clustered mode, all scheduler instances must run the same Quartz version, so if you had a cluster (multiple nodes), you would need to upgrade all nodes and coordinate downtime. In your case, with a single node, this isn’t a concern, but still ensure only one scheduler instance points to the database during the upgrade to avoid conflicts.

**How to check?** If you’re not sure how it’s configured (as you said “no idea how to check that”), locate the Quartz configuration:

* If using Spring’s `SchedulerFactoryBean`, it might be loading properties via `setQuartzProperties(...)` or a properties file on the classpath. Find that properties file or bean definition.
* Look specifically for `org.quartz.jobStore.isClustered` and `org.quartz.jobStore.class` keys in that config. This will tell you the mode and store type.

If the application was indeed single-node and non-clustered before, continue with that mode after the upgrade. (No special new settings are needed for single-node mode – just ensure clustering stays off.) If you discover it was clustered or might need clustering in the future, Quartz 2.3.2 supports it the same way 2.1.6 did. The upgrade steps below include the necessary DB changes that apply to both clustered and non-clustered use.

## 3. Upgrade the Database Schema (JDBC JobStore)

One of the biggest changes between Quartz 2.1.6 and 2.3.2 is an **update to the database schema** for JDBC JobStore. If your scheduler uses a database to persist job details and triggers, you **must apply schema changes** or Quartz 2.3.2 will error out. In particular, Quartz 2.2.0+ introduced a new column and other tweaks:

* **Add the `SCHED_TIME` column to the `QRTZ_FIRED_TRIGGERS` table.** This column stores the scheduled fire time of triggers (in milliseconds since epoch) to improve clustering/misfire handling. It’s a required NOT NULL field in Quartz 2.2+. If your database was set up for Quartz 2.1.6, this column is missing and **Quartz 2.3.2 will throw errors** on startup (e.g. “Unknown column ‘SCHED\_TIME’ in ‘field list’” when it tries to insert fired trigger records). You need to alter the table to add this column before running the new scheduler. For example:

  * **MySQL:** `ALTER TABLE QRTZ_FIRED_TRIGGERS ADD COLUMN SCHED_TIME BIGINT(13) NOT NULL;`
  * **Oracle:** `ALTER TABLE QRTZ_FIRED_TRIGGERS ADD SCHED_TIME NUMBER(19) NOT NULL`
  * **SQL Server:** `ALTER TABLE QRTZ_FIRED_TRIGGERS ADD SCHED_TIME BIGINT NOT NULL;`
    Use the appropriate SQL type for a 64-bit integer in your DB. (Quartz’s official suggestion for MySQL is BIGINT(13) which is sufficient for time in ms, but BIGINT(19) is also fine – the exact precision isn’t critical as long as it’s an 8-byte integer field.)

* **If your Quartz tables were originally created for Quartz 2.x (which they should have been for 2.1.6),** most other schema features are already in place (e.g. `SCHED_NAME` columns on each table, `isNonConcurrent` fields, etc., were introduced in Quartz 2.0). However, it’s wise to double-check if any other schema differences exist between your current tables and the Quartz 2.3.2 schema:

  * Quartz 2.x uses a `QRTZ_SIMPROP_TRIGGERS` table (for “simple property triggers”) that might not have existed in very early 2.0 versions. Your 2.1.6 likely already has it, but confirm that table’s presence. If it’s missing (unlikely), you’d need to create it (Quartz 2.3 expects it). The table stores simple triggers with primitive properties (as an alternative to blob data for complex triggers).
  * Quartz 2.3.1 made a minor update for **Sybase databases**: the `VARCHAR` length of trigger name columns was increased from 80 to 200. If you happen to use Sybase, you should alter your trigger name and group columns to length 200 to match the new schema. (For other databases, Quartz’s table scripts already used 120 or 200 length, so no change likely needed.)
  * Quartz 2.3.0 added a missing foreign key constraint for `QRTZ_BLOB_TRIGGERS` on Microsoft SQL Server. If you use SQL Server, consider adding that FK (linking `QRTZ_BLOB_TRIGGERS` to `QRTZ_TRIGGERS` on sched/name/group) for consistency. This won’t affect running Quartz, but it aligns the schema with the official script.

**How to get the correct schema scripts:** The Quartz distribution provides SQL scripts for each supported database under a `docs/dbTables` directory. You can obtain the Quartz 2.3.2 scripts (from the official Quartz website or Maven resource) for your database and compare them to your current schema. The main change from 2.1.6 to 2.3.2 is the addition of `SCHED_TIME`. Other differences may be new indexes or constraint names. It’s often simplest to apply an incremental SQL alteration rather than rebuilding the schema from scratch (especially since you likely have data in the tables that you want to keep).

**Performing the DB upgrade:** It’s crucial to do this carefully:

* Schedule downtime for the scheduler. **Shut down the Quartz scheduler** (the old 2.1.6 instance) cleanly before migrating. A clean shutdown (`scheduler.shutdown(true)` in code or via Spring’s `waitForJobsToCompleteOnShutdown=true`) will ensure there are no lingering entries in `QRTZ_FIRED_TRIGGERS` that violate the new NOT NULL constraint. Ideally, the `QRTZ_FIRED_TRIGGERS` table should be empty when you add the `SCHED_TIME` column (since it’s NOT NULL). If you cannot guarantee the table is empty (e.g., if you must add the column while jobs might have been mid-fire), you can provide a default value or set existing rows’ `SCHED_TIME` to equal their `FIRED_TIME` as a one-time fix. But the safest path is to ensure no triggers are running.
* **Back up your Quartz tables** before making changes. This way, if something goes wrong, you can restore the scheduler state.
* Run the SQL `ALTER` statements for your DB to add `SCHED_TIME` and any other needed adjustments. Double-check that the column was added successfully.
* (Optional but recommended) Update any indices or constraints per the new schema. For example, Quartz 2.x uses composite primary keys including `SCHED_NAME` on each table. If your existing schema was set up correctly for 2.1.6, you should already have those. Just verify primary keys and foreign keys match the 2.3.2 script. You may see in the official schema that `QRTZ_FIRED_TRIGGERS` primary key is (`SCHED_NAME`, `ENTRY_ID`) etc. – your DB should reflect that.

By applying the above, your database will be **forward-compatible** with Quartz 2.3.2. This addresses the critical schema change that would otherwise break the scheduler.

## 4. Code Changes and API Differences to Watch For

Quartz 2.3.2 is backward-compatible with 2.1.6 for the most part, but there are a few API changes and deprecations between these versions. Since you “didn’t build the application” originally, you’ll want to **search the codebase** for usages of certain Quartz APIs and adjust them if needed:

* **SchedulerListener interface change:** If the application uses Quartz listeners (for example, implementing `org.quartz.SchedulerListener` or registering one via `scheduler.getListenerManager()`), note that Quartz 2.2 introduced a new callback method in that interface. The method `schedulerStarting()` was added to `SchedulerListener` (in Quartz .NET it’s noted as `SchedulerStarting` as well). This means any custom `SchedulerListener` implementation will fail to compile/run until you implement the new method. In Java, the interface addition will cause a compile error if you have your own listener class. The fix is to implement `public void schedulerStarting()` (you can leave it empty or do any needed logic when the scheduler is starting). If you don’t have any custom listeners, this doesn’t affect you. (JobListeners and TriggerListeners were unchanged in 2.x, but recall that Quartz 2.x had already revamped how listeners are registered using Matcher rules – that change was from Quartz 1.x to 2.0. Since you were on 2.1.6, your code already should be using the 2.x listener APIs.)

* **DirectSchedulerFactory API change:** If the code uses `org.quartz.impl.DirectSchedulerFactory` to programmatically create a scheduler, be aware that one of the parameters was removed in Quartz 2.2. In 2.1.x you might see a call like `DirectSchedulerFactory.getInstance().createScheduler(schedName, instanceId, threadPool, jobStore, **dbFailureRetryInterval**, …)`. The `dbFailureRetryInterval` parameter (used for a retry pause if the DB is down) has been **removed** in newer versions. Quartz decided to drop it from the factory methods. So if your code uses DirectSchedulerFactory, you’ll need to call the newer method signature (without that parameter). In many cases, applications don’t use DirectSchedulerFactory at all (they use StdSchedulerFactory via config, or Spring’s SchedulerFactoryBean). But do a quick search for “DirectSchedulerFactory” in your project to be sure. If found, adjust the code to the new signature or remove the parameter.
  *(Related note: if using StdSchedulerFactory with a properties file – which is common especially with Spring – the `org.quartz.scheduler.dbFailureRetryInterval` property key is still recognized by StdSchedulerFactory for backward compatibility, but using it is generally unnecessary. The removal mainly impacts the DirectSchedulerFactory programmatic API.)*

* **Quartz “JobStoreSupport” changes (minor):** In 2.3, some internal improvements were made. For example, there were performance improvements in certain SQL queries and handling of misfires. You typically won’t need to change code for these. Just be aware if you had any custom subclass of `JobStoreSupport` (unlikely) or relied on internal behavior, things may be slightly different (mostly better). For instance, job recovery on startup was improved in 2.3.0, so if the scheduler dies in the middle of a job, 2.3.2 may handle the recovery more gracefully than 2.1.6 did.

* **New Scheduler features (optional usage):** Quartz 2.3.x added a few conveniences:

  * Ability to schedule a job with **multiple triggers in one call** (`scheduler.scheduleJob(jobDetail, Set<Trigger>, replace)` method). If you find code that was scheduling multiple triggers for the same job individually, you can leave it as-is; or refactor to use the new single-call method (not required, only if you want to take advantage of it).
  * Quartz 2.3 allows configuring the worker thread names via a system property or `SimpleThreadPool.setThreadNamePrefix` (so your threads can have a custom prefix). Again, not required to change – only if you want to utilize this feature for easier debugging.
  * There’s now support for **HikariCP** as a connection pool (Quartz 2.3.0 upgraded the default pooling options and added HikariCP support). If previously you were using C3P0 or another pool via Quartz, you might consider switching to HikariCP for better performance, but this is optional. Ensure the Quartz properties are updated accordingly if you do (the property `org.quartz.dataSource.someDS.provider = HikariCP` can be used). If you stick with your current DataSource (or if Spring is injecting the DataSource), no config change is needed – just be aware of the new option.
  * If the application used to rely on `JobDataMap` behavior: Quartz 2.x (including 2.1.6 and 2.3.2) by default stores job data map values by serializing non-String values. There’s a property `org.quartz.jobStore.useProperties` which if true, forces storing data as strings (for compatibility with certain setups). That behavior has not changed between 2.1.6 and 2.3.2. So no action needed unless you explicitly want to change it. Just ensure you keep the same setting as before to avoid any surprises with how job data is persisted.

* **Deprecated/removed constants or methods:** Check if the code references any Quartz constants or methods that might have moved. One example: In very old Quartz versions (pre-2.0) you had trigger constants in different places, but by 2.x those were unified. Since you were already on 2.1.6, you’re already using the 2.x API style (JobKey/TriggerKey, builders, etc.). There should be no major differences in 2.3.2. Methods like `scheduler.getTrigger(triggerKey)` or `getJobDetail(jobKey)` remain the same. The only tiny difference is Quartz 2.2+ added a `Scheduler.shutdown(boolean wait)` method override (you likely already use that). Most core APIs (scheduling jobs, defining JobDetail/Trigger via `JobBuilder`/`TriggerBuilder`) are identical between 2.1.6 and 2.3.2. Thus, your existing scheduling code should work without modification.

**Tip:** After updating the Quartz library, **run a full build and let the IDE/compiler show errors or warnings**. This will catch any places where methods no longer exist or interfaces need an extra method. Fix those as described above. Commonly, if any issue arises, it’s the SchedulerListener or DirectSchedulerFactory points mentioned. If no compile errors, that means the code didn’t use any changed APIs and should run fine.

## 5. Spring Framework and Integration Adjustments

Since you use Spring 5.3, it’s worth considering how Quartz integration is handled:

* If the application uses Spring’s `SchedulerFactoryBean` (from `org.springframework.scheduling.quartz`), you don’t need to change that code or XML config. The `SchedulerFactoryBean` will simply pick up Quartz 2.3.2 at runtime. Spring 5’s SchedulerFactoryBean is compatible with Quartz 2.x and will work the same as with 2.1.6. Just ensure that any Quartz properties you were setting (via `setQuartzProperties` or a properties file) are still correct for the new version. **All Quartz property names have stayed the same between 2.1.6 and 2.3.2**, so you shouldn’t need to change keys in your `quartz.properties`. For example, properties like `org.quartz.threadPool.threadCount`, `org.quartz.jobStore.misfireThreshold`, etc., remain valid. You may introduce new properties if you want (like the `org.quartz.threadPool.threadNamePrefix` if using SimpleThreadPool in 2.3), but none should be removed.
* If Spring was using any factory beans like `JobDetailFactoryBean`, `CronTriggerFactoryBean`, those are just wrappers around Quartz types. They will continue to produce `JobDetail` and `CronTrigger` objects for Quartz 2.3. No changes needed there. Just be sure to update the Quartz dependency so that these beans are now creating 2.3.2 JobDetails/Triggers (which they will automatically once the Quartz JAR is new).
* Regarding **Spring Integration** (if actually used in the app logic): Spring Integration’s Quartz support (for example, a Spring Integration message endpoint that fires on a Quartz schedule) should not require changes either. Spring Integration 5.x simply uses Quartz’s scheduling API under the hood. After upgrade, monitor any such integration to ensure it still triggers messages as expected. It’s rare to have issues here, but pay attention in testing if applicable.
* One thing to note: **Quartz 2.3.2 does not provide a “quartz-all” jar** (as you may have noticed). In older versions, some people included a `quartz-all-X.jar` which bundled everything. Now you include `quartz-2.3.2.jar` (and possibly `quartz-jobs-2.3.2.jar` if you need Quartz’s sample jobs). This mainly matters for ensuring all classes are present. For example, if Spring’s Quartz support was expecting to find `org.quartz.impl.StdSchedulerFactory` or others, those are in the main quartz jar, which you have. Just remove any old `quartz-all-2.1.6.jar` references to avoid conflicts, and use the official Quartz artifacts for 2.3.2.

## 6. Testing the Migrated Scheduler

After making the above changes, perform thorough testing:

* **Startup the application with Quartz 2.3.2** and watch the logs closely. On startup, Quartz will log its version and attempt to initialize the thread pool and job store. Verify that it starts without errors. In particular, look out for any `JobPersistenceException` or database errors on startup. An error like *“Couldn't acquire next trigger: Unknown column 'SCHED\_TIME'…”* means the DB schema wasn’t updated correctly – fix that by adding the column or correcting the schema. If you see errors about database constraints or primary keys, you may need to adjust those to match the Quartz 2.3 schema.
* If you have **existing jobs and triggers in the database**, ensure they were loaded and scheduled. Quartz 2.3.2 should read the existing `QRTZ_JOB_DETAILS` and `QRTZ_TRIGGERS` entries created under 2.1.6 without issue (the data formats are compatible). Your jobs should resume where they left off. For example, if you had a calendar or cron trigger that was stored, it should next fire according to its schedule.
* **Trigger firing:** Test that a sample job actually fires on schedule in the new version. This ensures that the scheduler thread is running and can execute jobs. The behavior of executions should be the same. One thing to double-check is misfire instructions: Quartz 2.3.2 uses the same misfire instruction constants and handling as 2.1.6 for SimpleTrigger and CronTrigger. The default misfire handling didn’t change. However, because of internal fixes, you might notice fewer misfire issues if any existed.
* **Shutdown and recovery:** If possible, test shutting down the new scheduler and starting it back up to ensure that persistent triggers recover correctly. Quartz 2.3.2 had fixes for job recovery on startup, so a job that was running at the time of shutdown might be handled slightly differently (more gracefully) than before. This isn’t usually something you see unless you had a crash; just know that the mechanism improved.
* **Performance and logging:** Quartz 2.3 introduced some performance tweaks (e.g., more efficient SQL queries, option to configure batch trigger acquisition). In a single-node simple setup, you may not notice a big difference, but if your load is high, observe if jobs are executing on time and thread pool usage is normal. The upgrade should not degrade performance; if anything, it may improve it modestly due to query improvements and the option of batch trigger acquisition (configurable via `org.quartz.scheduler.batchTriggerAcquisitionMaxCount`, off by default). You generally don’t need to change these settings unless you have specific needs.

During testing, also pay attention to any **Spring-related behaviors**:

* If using Spring’s scheduling annotations (`@Scheduled`) *alongside* Quartz, ensure they’re all still working (they operate separately from Quartz).
* If using a `SchedulerFactoryBean`, it typically autowires the DataSource. Make sure the DataSource is correctly set (it should be, if nothing changed in Spring config). Quartz 2.3.2 will use it the same way 2.1.6 did. You might see an info log from `org.quartz.impl.jdbcjobstore.JobStoreTX` saying “Using dataSource \[name]” – confirm it picks up your DataSource.

## 7. Additional Considerations

Finally, here are a few extra things to keep in mind for a smooth migration:

* **Backup and Rollback Plan:** Since you are not the original developer and are unsure of all usage, do this upgrade in a lower environment first. Backup the database before applying changes. Verify all jobs run correctly. In case of unexpected issues, be ready to revert to Quartz 2.1.6 and the old schema. (Quartz 2.3.2 should not corrupt or change data in a way that 2.1.6 can’t read, except the new SCHED\_TIME field which 2.1.6 would simply ignore if it exists. So rollback would mainly involve redeploying the old version and perhaps dropping the SCHED\_TIME column if 2.1.6 complains – which it typically wouldn’t, it would just not use that column.)
* **Check for any Terracotta or clustering addons:** Quartz 2.x had an optional Terracotta job store for clustering (in Quartz 2.1 days). If by chance your project used that (look for Terracotta classes or `JobStoreTC` in config), note that Quartz 2.3 might not support the old Terracotta OSS clustering (Terracotta support was tied to Quartz versions up to 2.2). However, given you said single node, this likely doesn’t apply.
* **Quartz Plugins:** If the application configured any Quartz plugins (like the `LoggingJobHistoryPlugin`, `LoggingTriggerHistoryPlugin`, or others via `org.quartz.plugin.` properties), those plugins are still available and work the same in 2.3.2. No changes needed there. Just ensure the plugin classes are on classpath (they are included in quartz 2.x JAR). One small fix in Quartz 2.3.1 was a typo in `QuartzInitializerListener` (used in web apps to start Quartz on startup) – if you use that listener (defined in `web.xml` or Spring), you might not even notice the typo, but upgrading Quartz will implicitly fix it.
* **Spring transaction integration:** If your Quartz is configured with a DataSource and `transactionManager` (Spring’s support for managing Quartz transactions), that should continue to work. Quartz 2.3 did not change anything in the JobStoreTX vs CMT behavior. Just verify that if you commented out or changed anything around `nonTransactionalDataSource` or `transactionManager` in the config, it’s as desired. The snippet you provided in the question (Spring config) suggests they might be using `nonTransactionalDataSource` for Quartz. This is okay and likely remains as-is.

## 8. Summary

Perform the upgrade step by step: update the library, adjust the database, adapt any code for minor API changes, and then test thoroughly. To recap the critical points:

* **Bump Quartz to 2.3.2** in your build and ensure Spring picks up the new version.
* **Apply DB schema changes**: primarily, add the `SCHED_TIME` column to `QRTZ_FIRED_TRIGGERS` (and check for any other schema updates).
* **Check configuration**: remain in single-node mode (clustering off) unless needed, and use the same JobStore (likely JDBC) with the updated schema.
* **Adjust code for API changes**: implement the new listener method if you have custom `SchedulerListener` (to handle `schedulerStarting()`) and remove any deprecated DirectSchedulerFactory params. Most Quartz API usage will remain the same.
* **Leverage improvements**: Quartz 2.3.2 brings many bug fixes and some new features (e.g., improved clustering, new scheduling methods, better performance) while staying compatible with your setup. You don’t have to use the new features immediately, but it’s good to know they exist (for example, the ability to use HikariCP if you need a robust connection pool, or the convenience of scheduling multiple triggers together).

By following these steps, you should be able to migrate from 2.1.6 to 2.3.2 smoothly. The key is to **migrate the database** and update the code for the few breaking changes introduced in Quartz 2.2.0. After that, Quartz 2.3.2 should operate as a drop-in replacement, and you can enjoy a more up-to-date scheduler with potential bug fixes and performance enhancements. Good luck with the migration!

**Sources:**

* Quartz 2.2.0 Release Notes (database schema changes and API updates)
* Quartz Official Documentation – Changelog and release highlights for 2.3.x
* Stack Overflow – Known schema update (`SCHED_TIME` column addition) when upgrading Quartz
* Quartz Scheduler Migration Guide (for reference on schema and API differences from older versions)
* Quartz Scheduler Documentation – Using JDBC JobStore and table creation scripts
