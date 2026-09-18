# US Stock & Crypto Investing — Tax Implications, US vs India

> Last updated: 2026-09-18 · Verified against current law

**Scope of this doc:** how your **US-side investments** (brokerage stocks, crypto, and by pointer 401(k)/Roth/HSA) are taxed (a) while you live in the US and (b) after a permanent move back to India — including the RNOR window strategy. India's taxation of your *Indian* assets: `NRI Taxation Overview.md`. US reporting of Indian assets: `US India Tax Compliance.md`. Retirement-account depth: sibling docs `401K HSA Tax Scenarios.md` and `HSA After Moving to India.md`.

---

## What changed recently (2025–2026)

- **OBBBA (Jul 2025):** TCJA brackets permanent; 2026 LTCG breakpoints — 0% up to **$49,450** single ($98,900 MFJ), 15% to **$545,500**, 20% above; +3.8% NIIT over $200k MAGI single. (https://taxfoundation.org/data/all/federal/2026-tax-brackets/)
- **India (since 23 Jul 2024, reaffirmed through Budget 2026):** foreign (unlisted-in-India) shares held by an Indian **resident**: LTCG after **24 months** at **12.5% without indexation**; STCG at slab. Crypto stays **30% flat**, no loss offset.
- **US estate tax exemption $15M (2026, permanent, indexed)** — but that's for US-domiciled persons; a non-resident non-domiciliary gets only **$60,000** on US-situs assets. This asymmetry is the single biggest post-move trap for a large US brokerage account.
- **No US–India treaty renegotiation pending**; portfolio-dividend treaty cap remains **25%**.

---

## 1. While you live in the US (resident alien)

You're taxed exactly like a citizen on investment income:

| Item | 2026 US treatment |
|---|---|
| Qualified dividends | 0/15/20% (same breakpoints as LTCG) |
| LTCG (>1 yr) | 0% ≤ $49,450 · 15% ≤ $545,500 · 20% above (single, taxable income) |
| STCG (≤1 yr) | Ordinary rates (10–37%) |
| NIIT | +3.8% on net investment income once MAGI > $200,000 single / $250,000 MFJ |
| Crypto | Property — same CG rules; every swap/spend is a disposal; wash-sale rule still does **not** apply to crypto as of 2026 (proposals recur — watch) |
| Tax-loss harvesting | Allowed; $3,000/yr net loss vs ordinary income, rest carries forward |

India taxes none of this while you're NRI — US-source investment income of a non-resident is outside Indian scope. Simple years: one country per asset class.

**MFJ vs MFS:** filing jointly almost always wins on CG breakpoints ($98,900 0%-band vs $49,450 each but MFS gets penalized brackets elsewhere). MFS is only worth modeling when one spouse has income-driven reasons.

## 2. After the move: US side (you become a nonresident alien)

Timeline mechanics first: in the departure year you're **dual-status** (resident until your residency-termination date, NRA after); substantial presence often keeps you a US tax resident for that whole calendar year. Plan sales around the status change, not the flight date.

Once you're an NRA holding a US brokerage account:

| Item | NRA treatment |
|---|---|
| **Capital gains on US stocks** | **Not US-taxed at all** (unless you're physically in the US ≥183 days that year — then 30% flat). Sell as an NRA and the US collects nothing. |
| **Dividends** | 30% statutory withholding → **25% under the US-India treaty** for portfolio holders. File **W-8BEN** with the broker (cite treaty Article 10(2)(b)); renew every 3 years. |
| **Interest** | Bank-deposit interest and most portfolio interest: exempt for NRAs. |
| **Crypto gains** | Generally not US-source for an NRA — not US-taxed (same 183-day caveat). |
| **Broker logistics** | Many brokers (Schwab, IBKR, Fidelity to a degree) support India-resident NRA accounts; some (Robinhood) force liquidation. Confirm before moving; Kraken similarly — check their India policy. |
| **Estate tax** | **US-situs assets (US stocks, even at a foreign broker) above $60,000 face up to 40% estate tax for an NRA non-domiciliary. No US-India estate treaty.** US-listed *foreign*-domiciled funds (e.g., Ireland UCITS) and bank deposits are non-US-situs — the classic mitigation. |

## 3. After the move: India side

| Phase | India taxes your US portfolio? |
|---|---|
| **RNOR years (~first 2–3 FYs)** | **No** — foreign-source dividends and capital gains are exempt for RNOR (unless from a business controlled in India). |
| **ROR (ordinarily resident)** | **Yes, worldwide:** US dividends at slab (with FTC via Form 67 for the 25% US withholding, capped at your Indian rate on that income — at slabs below 25% part of the US withholding is stranded); US stock LTCG (>24 mo) at 12.5%, STCG at slab; **crypto at flat 30% + cess, no loss offset, no expense deduction**; Schedule FA disclosure of every US account/asset becomes mandatory (Black Money Act penalties for misses). |

**The RNOR harvest:** the window where the US no longer taxes your gains (NRA) *and* India doesn't yet (RNOR) is a genuine, legal **zero-capital-gains-tax corridor** for your appreciated US stocks and crypto. Sell, reset basis (rebuy if you want the exposure), and re-enter ROR years with stepped-up cost. This is the highest-value tax move available to you; sequence it deliberately — see §5.

**401(k)/Roth IRA/HSA:** distributions have their own treaty and India-recognition problems (India doesn't recognize Roth/HSA wrappers for residents; §89A deferral election exists for recognized retirement accounts like 401(k)). Full scenarios live in `401K HSA Tax Scenarios.md` and `HSA After Moving to India.md` — the RNOR window is also the cheapest time for any planned Roth conversions or HSA reimbursement claims.

## 4. Worked example (move back mid-2028, single)

- 2026–27 (US resident): $40k LTCG realized → 15% federal + state; India: nothing.
- Departure year 2028: dual-status — realize nothing big after the residency-termination date until NRA status is clean.
- FY 2028-29 → FY 2030-31 (RNOR, NRA): sell $300k of appreciated US stock + crypto → **US: $0 (NRA, <183 days in US), India: $0 (RNOR)**. Rebuy what you want to keep. File W-8BEN so dividends are withheld at 25% not 30%.
- FY 2031-32 (ROR): fresh basis; future LTCG at India 12.5%; dividends at slab with 25% US FTC; crypto now 30% flat in India — consider exiting crypto entirely during RNOR.
- Throughout NRA years: keep US-situs holdings mindful of the $60k estate-tax cliff (term insurance or non-US-situs wrappers if the account stays large).

## 5. Action items / decision points

1. **While in the US:** harvest losses annually; keep MAGI vs the $200k NIIT line in view when realizing gains; prefer >1-yr holdings for the 15% rate.
2. **Keep meticulous basis records now** (broker CSVs, crypto tx exports) — India will need USD→INR basis for post-RNOR sales, and Schedule FA wants acquisition data.
3. **Before the move:** confirm your broker and Kraken support India-resident NRA accounts; open an IBKR-type fallback while you still have a US address if not.
4. **Departure year:** get the dual-status boundary right; file W-8BEN immediately after; avoid 183+ US days in any NRA year you realize gains.
5. **RNOR window:** execute the gain harvest (stocks + especially crypto, given India's 30% regime); do planned Roth conversions/withdrawal sequencing per the 401k/HSA sibling docs; time the return date to maximize full RNOR years.
6. **Watch:** crypto wash-sale proposals in Congress; the pending CBDT notification on Budget 2026's 5-year returning-professional foreign-income relief (could extend the corridor beyond RNOR); estate-tax exposure once the brokerage account exceeds ~$60k post-move.
