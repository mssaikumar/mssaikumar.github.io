# US Tax Compliance for Indian Assets & Income (H-1B Resident Alien)

> Last updated: 2026-09-18 · Verified against current law

**Scope of this doc:** what the *US* requires you to report and pay on your Indian assets and income while you're a resident alien (substantial presence on H-1B). India's own taxation of those assets: `NRI Taxation Overview.md`. US-stock scenarios and the move-back transition: `US India Tax Implications.md`. Moving money: `us-india-remittance-tax-guide.md`.

---

## What changed recently (2025–2026)

- **OBBBA (Jul 2025)** made TCJA rates/brackets permanent — no 2026 rate cliff. 2026: standard deduction **$16,100 single / $32,200 MFJ**; top 37% bracket above $640,600 single; SALT cap **$40,400** (phases back to $10k above ~$505k MAGI). (https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill)
- **FBAR penalties inflation-adjusted for 2026:** non-willful up to **~$16,536 per violation**; willful the greater of ~$165,353 or 50% of the account balance. Thresholds themselves unchanged ($10,000 aggregate).
- **India side:** Income-tax Act 2025 effective 1 Apr 2026 (Form 15CA/15CB become 145/146); Budget 2026 opened a 6-month foreign-asset amnesty *for Indian residents* — not you yet, but relevant the year you return.
- **No US–India treaty renegotiation** as of 2026 — the 1989 DTAA (amended 2000) stands.

---

## 1. Baseline: you're taxed like a citizen

As a resident alien you report **worldwide income** on Form 1040: NRO interest, **NRE interest (exempt in India but fully taxable in the US — no FTC because India charged nothing)**, FCNR interest, Indian dividends, rent, capital gains, and interest on money you've lent to people in India. Convert at the yearly average rate (IRS/Treasury rates) for income; spot rates for one-off sales.

Commonly missed on the 1040:
- **NRE/FCNR interest** ("it's tax-free" — only in India).
- **Interest on personal loans to friends/family in India** — taxable as ordinary interest income. If you charge no interest, US **imputed-interest (AFR) rules** can apply to loans over $10,000; document loans in writing.
- **Indian bank FD interest accrued but not paid out** — cash-basis taxpayers report when credited; Indian banks credit quarterly/annually, so it *is* being credited.
- **Schedule B Part III** — you must tick "yes" to foreign accounts every year and name India.

## 2. FBAR — FinCEN Form 114

| Item | Rule (2026) |
|---|---|
| Trigger | Aggregate of all foreign financial accounts **> $10,000** at *any moment* in the calendar year |
| What counts | NRE, NRO, FCNR, Indian brokerage/demat, Indian mutual fund folios, PPF/EPF accounts, LIC policies with cash value, accounts you merely have **signature authority** over (e.g., joint with parents) |
| Where | FinCEN's BSA e-filing site — *not* with the 1040 |
| Deadline | Apr 15, automatic extension to Oct 15 |
| Penalties | Non-willful ~$16,536/violation (post-*Bittner*, per **report** not per account); willful: greater of ~$165,353 or 50% of balance, criminal exposure |

The $10,000 is the *sum across accounts converted to USD* — one ₹9 lakh FD alone crosses it.

## 3. FATCA — Form 8938 (filed with the 1040)

| Filing status, living in US | Trigger |
|---|---|
| Single | > $50,000 at year-end **or** > $75,000 anytime |
| MFJ | > $100,000 year-end or > $150,000 anytime |

Covers everything FBAR covers **plus non-account assets**: Indian shares held directly (not in an account), and — directly relevant to you — **promissory notes / money lent to Indian residents held for investment**. Your loans to others in India belong on 8938 once you're over the threshold. Penalty: $10,000 automatic, to $50,000 after IRS notice, plus a 40% accuracy penalty on tax from undisclosed assets. **8938 does not replace FBAR — file both.**

## 4. The PFIC trap — Indian mutual funds (and why you hold stocks, not funds)

Every Indian mutual fund/ETF is a **Passive Foreign Investment Company** to the IRS:

- Default §1291 treatment: gains/"excess distributions" are thrown back over your holding period, taxed at the **top ordinary rate (37%)** per year, **plus interest charges** — no LTCG rate, ever. Losses aren't deductible.
- **Form 8621 per fund per year** once holdings exceed $25,000 aggregate ($50,000 MFJ) — and always in a sale year.
- **QEF election:** effectively unavailable — no major Indian AMC (SBI, HDFC, ICICI Pru, Axis, Mirae) issues the required PFIC annual information statement.
- **Mark-to-market election:** only for "regularly traded" holdings — arguable for Indian listed ETFs, not for open-end funds; and it converts all gains to ordinary income anyway.

**Standing best practice:** as a US resident, hold **individual Indian stocks** (not PFICs) or nothing; if you still own Indian MFs, get transaction-level statements (CAMS/KFintech CAS) and price the exit — often the cleanest move is selling during a low-income year or **after returning to India and losing US-resident status** (but note the year of departure is usually still a full/dual-status US year). Direct Indian equities are fine: normal capital-gain treatment in the US, with FTC for Indian tax.

**EPF/PPF:** no treaty protection — the US taxes yearly accretions (conservative and prevailing position: employer contributions + interest are current income; PPF interest is US-taxable despite Indian exemption). Both are FBAR/8938-reportable. Don't extend a matured PPF as an NRI (not permitted anyway).

## 5. Foreign tax credit — Form 1116

- Indian tax actually paid (TDS u/s 195 on NRO interest, dividend TDS, capital-gains TDS) credits against US tax on the *same income*, limited to the US rate on that income basket (passive).
- **Fiscal-year mismatch:** India's FY is Apr–Mar; the US is calendar-year. Elect to credit taxes **paid (cash basis)** during the calendar year, or accrued — pick one method and stay consistent.
- Excess Indian tax (e.g., 30% NRO TDS vs your lower effective US rate) carries back 1 year / forward 10 — but a same-basket excess often never gets used; better to file the Indian ITR and get the excess TDS **refunded in India** (then reduce the FTC accordingly — a later Indian refund of credited tax requires re-determining the FTC).
- India-side treaty claims need IRS **Form 6166** (request via Form 8802, ~$85 fee, takes weeks) + India Form 10F.

## 6. Selling Indian assets while a US resident

- **Indian stocks:** India taxes first (20% STCG / 12.5% LTCG, see `NRI Taxation Overview.md`); US taxes the same gain at your US rates (LTCG 0/15/20% if held >1 yr — note **India's 12-month equity clock ≠ US 12-month clock** measured from actual trade dates, and the USD-basis gain differs from the INR gain because of FX movement). Claim FTC for Indian tax.
- **Indian property:** buyer withholds TDS on the *sale price* — expect a large refundable excess; India LTCG 12.5% (no indexation for NRIs); the US taxes the USD gain — a rupee that depreciated since purchase often makes the USD gain smaller than the INR gain (occasionally a USD loss while India still taxes a gain — FTC may not fully absorb it).
- Repatriating the proceeds: `us-india-remittance-tax-guide.md` §5 (NRO $1M route, 15CA/CB → 145/146).

## 7. Penalty exposure & fixing past misses

- Never filed FBAR/8938 but paid all tax: **Delinquent FBAR submission** procedures (no penalty if reasonable cause and no unreported income).
- Unreported Indian income too: **Streamlined Domestic Offshore Procedures** — 3 amended returns + 6 FBARs + 5% Title 26 penalty on the highest year-end foreign balance; requires non-willful certification. Far cheaper than examination.
- India-side symmetric risk arrives when you become resident again (Schedule FA + Black Money Act) — the Budget 2026 amnesty window is the template for how expensive skipping it is (30% + 90% penalty regime).

## 8. Action items / decision points

1. **Inventory every Indian account/asset now** (NRE, NRO, FDs, demat, any MF folios, PPF/EPF, LIC, loans made) with year-max balances — this is your FBAR/8938 worksheet.
2. **Confirm FBAR + 8938 have been filed for every year over threshold**; if not, use delinquent/streamlined procedures *before* any IRS contact.
3. **If you hold any Indian mutual funds: price the PFIC exit this year.** Individual Indian stocks are fine; funds are not.
4. **Put loans to individuals in India in writing** (principal, rate ≥ AFR, schedule) and report the interest on both returns; include the notes on Form 8938.
5. **Each spring:** report NRE/NRO/FCNR interest and Indian dividends on the 1040; attach Form 1116 for Indian TDS; tick Schedule B Part III.
6. **Watch:** 2026 FBAR penalty figures adjust annually; the India Budget 2026 amnesty mechanics (relevant on return); any future DTAA protocol news (none pending as of Sep 2026).
