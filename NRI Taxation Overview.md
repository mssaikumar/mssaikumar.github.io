# NRI Taxation Overview — How India Taxes NRIs vs Residents

> Last updated: 2026-09-18 · Verified against current law

**Scope of this doc:** how *India* taxes you — as an NRI today (H-1B, US tax resident) and as a returning resident later. For the US side of reporting Indian assets, see `US India Tax Compliance.md`. For US-stock scenarios, see `US India Tax Implications.md`. For moving money, see `us-india-remittance-tax-guide.md`.

---

## What changed recently (2025–2026)

- **Income-tax Act, 2025 replaces the 1961 Act from 1 April 2026** (Tax Year 2026-27 onward). It's mostly a renumbering/simplification — residency tests, NRI source rules, and DTAA access are preserved. "Previous year/assessment year" is replaced by a single **"tax year"**. FY 2025-26 returns (filed in 2026) are still under the 1961 Act. (https://www.pib.gov.in/PressReleasePage.aspx?PRID=2221416)
- **Budget 2025:** new-regime basic exemption raised to ₹4 lakh; §87A rebate makes income up to ₹12 lakh tax-free — **but the rebate is residents-only; NRIs never get it**.
- **Budget 2026 (Feb 2026):** slabs and capital-gains rates unchanged. TCS on LRS education/medical cut to 2% (from Apr 2026); NRI single-company listed-equity holding limit raised 5% → 10% (aggregate 24%, RBI notification 13 Jun 2026); a 6-month voluntary disclosure window for undeclared foreign assets; NRI property-sale TDS becomes PAN-based (no TAN) from 1 Oct 2026; a proposed **5-year foreign-income relief for returning professionals — conditions still pending CBDT notification, do not plan around it yet**.
- **Capital gains (since 23 Jul 2024, unchanged since):** STT-paid equity STCG **20%**, LTCG **12.5%** above ₹1.25 lakh/yr.

---

## 1. Residential status — the switch that decides everything

| Status | India taxes… |
|---|---|
| **Non-Resident (NRI)** | Only income received/accruing/arising in India |
| **RNOR** (resident but not ordinarily resident) | Indian income + foreign income *derived from a business controlled in India*; other foreign income exempt |
| **Resident & Ordinarily Resident (ROR)** | **Worldwide income** |

**You are resident for a financial year (Apr–Mar) if:**
1. In India **≥ 182 days** that year, **or**
2. In India ≥ 60 days that year **and** ≥ 365 days in the prior 4 years.

**Carve-outs that matter to you (Indian citizen working abroad):**
- While employed abroad, the 60-day test relaxes to 182 days for you on visits — **except**: if your India-sourced income exceeds **₹15 lakh**, a **120-day rule** applies: 120–181 days in India + ≥365 days in prior 4 years makes you a resident, but only **RNOR** (not ROR).
- **Deemed residency (§6(1A)):** an Indian citizen with India-source income > ₹15 lakh who is "not liable to tax in any other country" is deemed resident (RNOR). While you're a US tax resident this cannot hit you — you are liable to tax in the US.

**Practical rule while on H-1B:** keep India visits under 120 days per FY (under 182 if your Indian income stays below ₹15 lakh) and you remain NRI.

### RNOR — your landing pad when you move back
You qualify as RNOR (instead of ROR) for a year if **either**:
- You were NRI in **9 of the 10** preceding years, **or**
- You spent **≤ 729 days** in India in the preceding 7 years.

Typically gives a returning NRI **2–3 financial years** where foreign income (US dividends, capital gains, 401(k) growth, NRE/FCNR interest) stays out of Indian tax. Timing your return date early vs late in a financial year can add or subtract a whole RNOR year — model it before booking the one-way ticket. Details of what to do inside the window: `US India Tax Implications.md` §5.

---

## 2. Slabs and rates

### New regime (default) — FY 2025-26 and FY 2026-27 (unchanged by Budget 2026)

| Taxable income | Rate |
|---|---|
| Up to ₹4,00,000 | Nil |
| ₹4–8 lakh | 5% |
| ₹8–12 lakh | 10% |
| ₹12–16 lakh | 15% |
| ₹16–20 lakh | 20% |
| ₹20–24 lakh | 25% |
| Above ₹24 lakh | 30% |

Plus 4% health & education cess; surcharge from ₹50 lakh (10%) up to 25% cap above ₹2 crore under the new regime.

### Resident vs NRI — the gaps that bite

| Item | Resident | NRI |
|---|---|---|
| §87A rebate (income ≤ ₹12 lakh tax-free, up to ₹60,000 rebate) | Yes | **No — NRIs excluded** |
| Basic exemption offset against §111A/112A equity gains | Yes | **No** |
| Senior-citizen slabs (old regime) | Yes | No |
| Old-regime deductions (80C, 80D etc.) | Yes | Mostly yes, but new regime usually wins |
| ₹75,000 standard deduction (new regime, salary) | Yes | Yes, if Indian salary income |

**Example:** ₹9 lakh of NRO interest + Indian dividends in FY 2025-26. A resident with the same income pays ~₹0 (87A rebate). You as NRI pay: 5% on ₹4–8L (₹20,000) + 10% on ₹8–9L (₹10,000) = ₹30,000 + cess ≈ **₹31,200**.

---

## 3. Taxation by income type (your actual asset mix)

| Income | India tax while NRI | TDS |
|---|---|---|
| **NRE savings/FD interest** | **Exempt** (§10(4), while NRI under FEMA) | None |
| **FCNR deposit interest** | **Exempt** | None |
| **NRO interest** | Slab rates | **30% + surcharge + cess u/s 195** (≈31.2%+) |
| **Indian dividends** | 20% + cess u/s 115A (below the 25% DTAA cap, so domestic rate applies) | 20%+ |
| **Listed equity STCG** (STT paid, ≤12 mo) | **20%** flat (§111A) | Broker/buyer withholds for NRIs |
| **Listed equity LTCG** (>12 mo) | **12.5%** above ₹1.25 lakh/yr (§112A — the ₹1.25L exemption *does* apply to NRIs; the basic-exemption offset does not) | Yes |
| **Interest on money you've lent to individuals in India** | Slab rates (India-sourced). Borrower should technically deduct TDS u/s 195 at 30%+ when paying a non-resident — rarely done in informal loans; the income is still reportable in your ITR | 30%+ in theory |
| **Property rent** | Slab rates (30% standard deduction on NAV) | Tenant must withhold 30%+ |
| **Property sale LTCG** (>24 mo) | 12.5% without indexation (post-23-Jul-2024 sales; the 20%-with-indexation option for pre-Jul-2024 purchases is residents-only) | Buyer withholds on sale u/s 195; PAN-based (no TAN) from 1 Oct 2026 |

All of the above is *also* taxable on your US return while you're a US resident — India withholding becomes a Foreign Tax Credit there. Mechanics in `US India Tax Compliance.md`.

**Mutual funds:** Indian MFs are taxable in India like the tables above (equity funds follow 111A/112A; debt funds bought after Apr 2023 are slab-taxed) — but for a US resident they are **PFICs**, which is a US-side problem big enough that the standing advice is *don't hold Indian mutual funds while a US tax resident*. See `US India Tax Compliance.md` §4.

---

## 4. Compliance while NRI

- **ITR filing** required if Indian gross income > basic exemption (₹4 lakh new regime), or to claim TDS refunds (30% NRO TDS usually over-withholds vs slab). Due date ~31 July (belated/revised windows extended to 12 months by Budget 2026). ITR-2 today; a simplified **ITR-NRI form is expected** under the 2025 Act.
- **Schedule FA (foreign assets)** is for residents/RNORs, not NRIs — becomes relevant the year you return. Budget 2026 opened a **6-month amnesty** for previously undisclosed foreign assets (Black Money Act exposure otherwise: 30% tax + 90% penalty + prosecution).
- **Accounts under FEMA:** as an NRI your Indian savings accounts must be redesignated NRO; NRE/FCNR are your repatriable accounts. On return, redesignate to resident accounts (or RFC for foreign-currency funds — RFC interest stays exempt while RNOR).
- **TDS refunds:** file the ITR; lower/nil-TDS certificates (§197) are available if income is predictably below slab thresholds.
- **DTAA:** to claim treaty rates in India you need a US **Tax Residency Certificate (IRS Form 6166**, requested via Form 8802) + Form 10F filed online.

---

## 5. Action items / decision points

1. **Count your India days each FY** (Apr–Mar, not calendar year). Stay < 120 days if Indian income could exceed ₹15 lakh.
2. **File an Indian ITR every year you have NRO interest, lending interest, or Indian capital gains** — the 30% NRO TDS is almost certainly more than your slab liability; the refund is free money.
3. **Confirm your Indian bank accounts are properly NRO/NRE-designated** — a still-"resident" savings account is a FEMA violation and muddies the NRE tax exemption.
4. **Declare the interest on money lent to friends/family in India** in both ITR and the US return — it's the item most likely to be forgotten, and it's a Form 8938-relevant asset in the US (see `US India Tax Compliance.md`).
5. **Before moving back:** compute your RNOR window (9/10-year and 729-day tests) against candidate return dates; keep evidence of NRI years (passport stamps, US tax returns).
6. **Watch:** CBDT notification on the Budget 2026 "5-year foreign income relief" for returning professionals — if notified with workable conditions it could extend your effective RNOR-like shelter; the 2025 Act's new form numbers (Form 16→130, 26AS→168, 15CA/CB→145/146) from Apr 2026.
