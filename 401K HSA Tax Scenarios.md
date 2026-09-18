# 401(k) / IRA / Roth / HSA Withdrawal Tax Scenarios

> Last updated: 2026-09-18 · Verified against current law (OBBBA, SECURE 2.0, IRS 2026 inflation figures, India Income-tax Act 2025)

**Who this is for:** Indian citizen on H-1B, currently a US tax resident, holding a **Traditional 401(k), Roth IRA, and HSA**. May stay in the US indefinitely or return to India permanently in 1–5+ years. This doc maps every withdrawal scenario: stay in a no-tax state, stay in an income-tax state, or return to India (as a nonresident alien / Indian resident), plus the timing strategies that actually move the needle.

> **What changed recently (2025–2026)**
> - **OBBBA (July 2025)** made the TCJA rates/brackets **permanent** — no 2026 sunset. 2026 standard deduction: **$16,100 single**. Low-income-year withdrawal math below uses these numbers.
> - **2026 limits:** 401(k) deferral **$24,500** (catch-up $8,000; ages 60–63 $11,250); IRA **$7,500** (catch-up $1,100); HSA **$4,400 self / $8,750 family**. Mandatory *Roth* catch-up for prior-year wages above ~$145–150k (indexed) starts 2026 — irrelevant until age 50.
> - **SECURE 2.0 penalty exceptions now live:** $1,000/yr emergency expense, domestic abuse (~$10,000 indexed), terminal illness, federally declared disaster ($22,000), birth/adoption ($5,000), and from Dec 2025 up to $2,500/yr for long-term-care insurance premiums.
> - **India:** the **Income-tax Act, 2025** replaced the 1961 Act effective **April 1, 2026**. Section 89A (foreign retirement account relief) is renumbered **Section 158**; the mechanics (Rule 21AAA, Form 10-EE) carry over. New-regime slabs: effectively **no Indian tax up to ~₹12 lakh** (rebate), top slab 30% above ₹24 lakh + 4% cess.
> - **India still has no inheritance/estate tax** (checked Sep 2026) — but the US estate-tax trap for NRAs is real (see final section).

---

## 1. The four layers of cost on any early withdrawal

Every scenario below is just these four layers stacked differently:

| Layer | Traditional 401(k)/IRA | Roth IRA | HSA |
|---|---|---|---|
| US federal income tax | Ordinary income on full amount | Contributions: never. Earnings: taxed if non-qualified | Qualified medical: $0. Non-qualified: ordinary income |
| US early penalty | 10% under 59½ (exceptions below) | 10% on earnings (and young conversions) only | **20%** on non-qualified, until **65** |
| US state tax | Only while resident of a taxing state (4 U.S.C. §114 protects nonresidents) | Same | CA/NJ don't recognize HSAs at all |
| India tax | Zero while NRI/RNOR; full slab tax once ROR (FTC for US *income* tax; **penalties are never creditable**) | India doesn't recognize Roth: earnings taxable once ROR | India taxes HSA growth annually once ROR |

**Key mental model:** the US *income tax* layer can usually be engineered down to near zero (low-income years, standard deduction, graduated NRA rates, treaty). The **10%/20% penalty layer only goes away via an exception, age, or waiting** — and India never credits it.

### 2026 US reference numbers (single filer)

| Item | 2026 |
|---|---|
| Standard deduction | $16,100 (NRAs get **$0** — the India-treaty standard deduction is for students/apprentices only, not returning workers) |
| 10% bracket | up to $12,400 taxable |
| 12% bracket | $12,400 – $50,400 |
| 22% bracket | $50,400 – $105,700 |
| 24% bracket | $105,700 – $201,775 |

Source: https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill

### 10% penalty exceptions worth knowing (2026)

| Exception | 401(k) | IRA | Notes |
|---|---|---|---|
| Age 59½ | ✓ | ✓ | The clean exit |
| Rule of 55 | ✓ | ✗ | Separate from employer in/after the year you turn 55; only that employer's plan; **lost if rolled to an IRA** |
| SEPP / 72(t) | ✓ (after separation) | ✓ | Substantially equal payments for the longer of 5 years or until 59½; rigid, but works from India and may double as treaty "periodic pension" |
| Medical > 7.5% AGI | ✓ | ✓ | |
| First home ($10k lifetime) | ✗ | ✓ | Reason to roll 401(k)→IRA |
| Higher education | ✗ | ✓ | Reason to roll 401(k)→IRA |
| Health insurance while unemployed | ✗ | ✓ | |
| Emergency personal expense | ✓ | ✓ | $1,000/yr, repayable within 3 yrs (SECURE 2.0) |
| Terminal illness / disability / death | ✓ | ✓ | |
| **Leaving the USA** | ✗ | ✗ | **Not an exception. Moving to India does not waive the penalty.** |

---

## 2. Traditional 401(k) — scenario grid

| | Stay US, no-tax state (TX/FL/WA) | Stay US, CA (worst case) | Return to India (NRA) |
|---|---|---|---|
| Federal income tax | Ordinary rates on top of salary | Same | Graduated rates if ECI (typical for 401k), else 30% flat; **no standard deduction** |
| 10% penalty (<59½) | Yes | Yes | **Yes — still applies** |
| State income tax | None | Up to 13.3% marginal | **None** (4 U.S.C. §114 bars states from taxing retirement income of nonresidents — even ex-CA residents) |
| State penalty | None | **+2.5%** (FTB 3805P) | None |
| Withholding | 20% mandatory on cash-outs | 20% fed + CA default | **30% NRA withholding** unless valid W-8BEN treaty claim; reconciled on 1040-NR (refund if actual tax lower) |
| India tax | n/a | n/a | Zero while RNOR; full slab tax once ROR (FTC for US income tax) |
| Forms | 1099-R, Form 5329 | + CA FTB 3805P | 1042-S or 1099-R, **1040-NR** + 5329; Form 8833 if claiming treaty |

### The NRA / DTAA picture (the part that matters most)

- **US-India treaty, Article 20(1):** private **pensions** and **annuities** paid "in consideration of past employment" are taxable **only in the country of residence** (India). Article 20(2): US Social Security is taxable only by the US.
- **Periodic payments** (monthly/quarterly annuitized withdrawals, a 72(t) SEPP stream): strong position that Article 20 gives India the exclusive taxing right → file **W-8BEN** claiming treaty, US withholding drops toward 0%, pay only Indian tax.
- **Lump sums — genuinely disputed.** Two positions:
  - *Conservative (most custodians and many practitioners):* a one-shot cash-out is not a "pension"; the US taxes it (30% withholding, or graduated ECI rates on 1040-NR) and India also taxes it once ROR, with FTC. Plan on this outcome.
  - *Aggressive (OECD-commentary-based):* a lump sum *in lieu of* pension after cessation of employment can still be an Article 20 "pension" → residence-only taxation. Some advisers file 1040-NR + Form 8833 on this basis. Real audit risk; don't rely on it for large amounts without a cross-border CPA.
- The 10% penalty applies to NRAs. (There is a fringe argument that if a treaty excludes the income from US tax, the §72(t) penalty base is zero — untested for India lump sums; treat the penalty as owed.)
- **India side once ROR:** India taxes the **entire withdrawal — contributions + growth — at slab rates** (top 30% + 4% cess; surcharge above ₹50L). India does not track US basis. FTC under DTAA Article 25 for US income tax actually paid; **the 10% penalty and any state tax are not creditable**.
- **Section 89A → Section 158 (from Apr 2026) + Rule 21AAA + Form 10-EE:** lets an Indian resident defer Indian taxation of the US retirement account to the **year of withdrawal** (matching the US), instead of accrual taxation each year. US is a notified country. File Form 10-EE **before the ITR due date** of the first year you claim it; the election is **irrevocable** while you remain resident. This fixes the FTC timing mismatch — it does not reduce Indian tax.

### Worked example — $100,000 401(k), age 35

| Strategy | US cost | India cost | Total lost |
|---|---|---|---|
| **A. Lump sum while ROR in India** | ~$16.7k income tax (graduated ECI, no SD) + $10k penalty = **$26.7k** | ~₹88L taxed at slab ≈ ₹24L (~$27k), minus FTC ~$16.7k → ~$10k extra | **~$37k (37%)** |
| **B. Lump sum during RNOR window** | Same **$26.7k** | **$0** (foreign income exempt for RNOR) | **~$27k (27%)** |
| **C. $25k/yr over 4 RNOR years** | Each yr: ~$2.75k tax + $2.5k penalty → **$21k** | $0 | **~$21k (21%)** |
| **D. Wait to 59½, periodic payments, W-8BEN Art. 20** | ~$0 US (treaty) | Slab tax in withdrawal years (spread out, 89A/158 election) | India slab only — often the cheapest if you don't need the money early |
| **E. 72(t) SEPP started after return** | No penalty; treaty position for periodic payments plausible → little/no US tax | $0 during RNOR, slab after | Very low, but locks you in for ≥ max(5 yrs, to 59½) |

*(Assumes ~₹88/USD, 2026 brackets, new-regime slabs. C beats B only because graduated brackets reset each year.)*

---

## 3. Traditional IRA — differences from the 401(k)

Same federal/California/NRA treatment as above. What's different:

- **Withholding:** 10% default (waivable via W-4P) instead of the 401(k)'s mandatory 20% — while resident. As an NRA, 30%/W-8BEN rules are the same.
- **More penalty exceptions** (first home, education, health premiums while unemployed) — the main reason to **roll the 401(k) into an IRA when leaving the employer**.
- **Rollover is tax-free and penalty-free** (direct trustee-to-trustee). Do it **before leaving the US**: 401(k) plans force out small balances (<$1,000 cashed out; $1,000–$7,000 auto-rolled to an IRA of the plan's choosing), often refuse foreign addresses, and give you no withdrawal flexibility. An IRA at a custodian that tolerates foreign addresses keeps every strategy above available.
- Losing the Rule of 55 is the one cost of rolling — irrelevant if you'll be in India well before 55.
- India treats IRA withdrawals identically to 401(k) withdrawals (89A/158 election available).

---

## 4. Roth IRA

### US side (rules are residency-blind)

Withdrawals come out in a fixed order: **contributions → conversions → earnings**.

| Money | Tax | 10% penalty |
|---|---|---|
| Contributions | Never taxed | Never — withdrawable **anytime, any age, any country** |
| Conversions | Already taxed at conversion | 10% if withdrawn within 5 tax-years of that conversion and under 59½ |
| Earnings | Tax-free only if 59½+ **and** account ≥5 years old ("qualified") | 10% if non-qualified (exceptions apply) |

The 5-year clock for earnings starts Jan 1 of your **first** Roth contribution year — it keeps running while you live in India.

### India side — India does not recognize Roth

- Once **ROR**, India sees the Roth as an ordinary foreign investment account. The prevailing practitioner position: **contributions come back as non-taxable capital, but earnings/growth are taxable in India** even when the US calls the distribution qualified and tax-free. (A stricter reading taxes accrued income annually; positions vary — flagged as unsettled. The 89A/158 election arguably covers a Roth IRA as a "retirement benefits account" and defers to withdrawal — most advisers do make the election for Roths too.)
- **Strategy:** withdraw Roth **earnings** during the **RNOR window** if you want them — US-qualified (if 59½+5yr) *and* India-exempt = genuinely tax-free in both countries. If you'll be far from 59½ during RNOR, at minimum you can pull **contributions** tax- and penalty-free in both countries at any time.
- Keep contributing to the Roth up to the year you leave (2026 limit $7,500) — contributions are the most flexible cross-border money you have.

### Roth conversion ladder (before/around departure)

In any low-income year while still a US resident (sabbatical, part-year final year), convert Traditional → Roth up to the top of the standard deduction / 10–12% brackets. **No 10% penalty on conversion itself.** Example: convert $16,100 with no other income → $0 federal tax. Converting in a no-tax state (or after leaving CA) avoids state tax on the conversion. Conversions are effectively unavailable once you're an NRA — this is a **before-you-leave** play. Note India (once ROR) ignores the conversion and would still tax growth on withdrawal — the ladder kills the US tax layer, not the Indian one.

---

## 5. HSA (summary — full detail in "HSA After Moving to India")

- Qualified medical expenses: tax-free and penalty-free **at any age, in any country**. Non-qualified before **65**: ordinary income + **20% penalty** (worst penalty of any account; India credits neither the penalty nor recognizes the shelter).
- CA/NJ residents: state taxes HSA contributions and annual earnings (no state recognition). Leaving CA ends that.
- Once ROR in India, HSA growth is taxed annually by India; Section 89A/158 relief very likely does **not** cover HSAs (not a "retirement benefits account") — flagged position.
- Optimal: never take non-qualified HSA money before 65; run the receipts/reimbursement strategy; consider depleting via receipts during RNOR.

---

## 6. India residency timeline — the RNOR window is the whole game

| Status | How you get it | India taxes |
|---|---|---|
| **NRI** | Before you return / <182 days in India | Indian-source income only |
| **RNOR** | Resident, but NRI in ≥9 of prior 10 FYs, **or** ≤729 days in India in prior 7 FYs | Indian-source income only — **US 401(k)/IRA/Roth/HSA withdrawals and growth are exempt** (if not received in India / not from an Indian business) |
| **ROR** | Once you fail both RNOR tests | **Worldwide income** at slab rates + Schedule FA disclosure of every US account (Black Money Act penalties for misses) |

- After 6+ years abroad you typically get **2–3 fiscal years of RNOR** (India's FY = Apr–Mar; landing date matters — arriving early in a FY can effectively add a year).
- **Everything you want to realize cheaply — 401(k)/IRA staged withdrawals, Roth earnings, HSA drawdown, US brokerage capital gains — should be sequenced into the RNOR years.** The US side (NRA tax + penalties) still applies; the Indian layer is zero.
- Once ROR: make the **89A/158 (Form 10-EE)** election for the 401(k)/IRA so India taxes only on withdrawal, file **Schedule FA** every year, and claim FTC via **Form 67**.

---

## 7. State tax: leave first, withdraw second

- **4 U.S.C. §114 (P.L. 104-95, 1996)** prohibits any state from taxing "retirement income" (401(k), IRA, qualified plans) of a person who is **neither a resident nor domiciliary** of that state when received. Confirmed still in force. So CA **cannot** tax your 401(k) withdrawal after you've moved to India (or Texas) — even though the money was earned in CA.
- While still a CA resident: CA taxes the withdrawal at up to 13.3% **plus a 2.5% state early-distribution penalty**. NJ/NY tax it as income (no extra penalty).
- Practical rule: **take zero retirement distributions in your final part-year of CA/NJ residency.** Cleanly establish non-residency (move out, sever ties) before any withdrawal or Roth conversion. CA is aggressive about residency audits — document the departure date.
- The §114 protection does **not** extend to HSAs (not "retirement income") — but as a nonresident of CA with no CA-source income you have no CA filing anyway.

---

## 8. Estate-tax trap for NRAs (don't skip this)

- Once you're an NRA, your US estate-tax exemption collapses from ~$15M to **$60,000** of **US-situs assets**, taxed up to 40% above that. **401(k), IRA, Roth, HSA balances and US stocks all count as US-situs.** There is **no US–India estate tax treaty.**
- A $500k retirement stack + US brokerage could expose your heirs to a six-figure US estate tax if you die while resident in India.
- Mitigations: draw accounts down over RNOR/early-ROR years; keep beneficiaries updated (beneficiary designation avoids probate, **not** the estate tax); term life insurance to cover the exposure (life insurance proceeds on an NRA's life are not US-situs); long-term, hold non-US-situs assets instead.
- India currently has **no inheritance tax** (abolished 1985; no live proposal as of the Feb 2026 budget) — watch each Union budget.

---

## 9. Action items / decision points

**While in the US (every year):**
- [ ] Max the cheap space: 401(k) $24,500, HSA $4,400/$8,750, Roth IRA $7,500 (2026). Roth contributions are the most reversible cross-border dollars.
- [ ] Any low-income year (job gap, sabbatical): Roth-convert up to the standard deduction (~$16,100 tax-free in 2026).
- [ ] Keep every HSA medical receipt from day one (shoebox strategy).

**In the ~12 months before leaving the US:**
- [ ] **Roll the 401(k) to a Traditional IRA** at a custodian confirmed (in writing) to service India-resident accounts. Ask specifically: hold, sell, withdraw, W-8BEN processing, wire to India.
- [ ] Do a final-year **Roth conversion** sized to your part-year bracket — after leaving CA/NJ if applicable.
- [ ] Establish clean state non-residency **before** any distribution or conversion.
- [ ] Set up: US bank account you can keep, US mailing address (relative), US phone number ported to Google Voice for 2FA.
- [ ] Update beneficiaries on every account; price term life against the $60k NRA estate exemption.
- [ ] Land in India early in an Indian FY if you can — it can stretch the RNOR window.

**After returning (RNOR years — the golden window):**
- [ ] File **W-8BEN** with every custodian immediately (treaty claims + correct withholding).
- [ ] Sequence withdrawals into RNOR: staged 401(k)/IRA amounts sized to the low US brackets (~$12–25k/yr each costs ~11% tax + 10% penalty and zero Indian tax), Roth earnings if 59½+5yr, HSA receipt reimbursements.
- [ ] Decide lump-sum vs periodic for anything large; get a cross-border CPA opinion before relying on Article 20 for a lump sum.

**Once ROR:**
- [ ] File **Form 10-EE** (89A/§158 election) before the first ITR due date; Schedule FA every year; Form 67 for FTC.
- [ ] Stop expecting India to respect Roth/HSA shelters — position those accounts accordingly.

**Never:** cash out a 401(k) as a lump sum while ROR (Scenario A above — ~37% gone), or assume leaving the country waives the 10%/20% penalties (it doesn't).

Key sources: https://www.irs.gov/newsroom/401k-limit-increases-to-24500-for-2026-ira-limit-increases-to-7500 · https://www.irs.gov/retirement-plans/plan-distributions-to-foreign-persons-require-withholding · https://uscode.house.gov/view.xhtml?req=granuleid%3AUSC-prelim-title4-section114&num=0&edition=prelim · https://cleartax.in/s/section-89a · https://www.dineshaarjav.com/blog-detail/401k-withdrawal-nri-returning-to-india-tax-guide
