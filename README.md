# Fixed Income Valuation, Duration Hedging & Convexity

An Excel model that prices a bond two ways, measures its interest rate risk, hedges a $1,000,000 position with a second bond, and then tests the hedge under parallel yield shocks of up to 3% in either direction. It was built as an independent project at UMass Boston in March 2026 using real U.S. Treasury yields from FRED.

The question behind it: duration matching removes first-order rate risk, so what is left over, and why?

## Key results

| | Result |
|---|---|
| Flat-yield price (Bond A) | $1,050.03 |
| Term-structure price (Bond A) | $1,050.41, a 0.04% difference |
| Duration, Bond A (Macaulay / Modified) | 4.56 / 4.39 |
| Duration, Bond B (Macaulay / Modified) | 8.42 / 8.07 |
| Hedge | Short about 556 units of Bond B ($543,990) against $1,000,000 long Bond A |
| Unhedged P&L at a 3% shock | About $131,700 (duration estimate) |
| Duration-hedged residual at a 3% shock | About $0.02 |
| Convexity-adjusted residual at a 3% shock | About $8,560 |

## What the results show

Matching dollar duration brings the hedged P&L to almost zero across all 13 shock scenarios. That result is close to automatic, because the duration estimate is linear and the hedge is built to cancel it exactly.

Adding convexity shows what the linear view hides. Bond B has far more convexity than Bond A (80.08 against 24.54), so shorting it to match duration leaves the portfolio short convexity. The hedged position loses money whether yields rise or fall. The loss is about $238 at a 0.5% move and grows to about $8,560 at 3%.

## Method

1. **Yield curve.** Treasury constant maturity yields (DGS3MO, DGS6MO, DGS1, DGS2, DGS5, DGS10, DGS30) from FRED. The 3-year and 4-year points were not in the series, so they were estimated by linear interpolation at 3.80% and 3.84%. The curve is partly inverted, with the 3-month yield above the 1-year yield.
2. **Pricing.** Bond A (5-year, 5% coupon, annual) is discounted at one flat yield, then again at a maturity-specific Treasury yield for each cash flow.
3. **Risk measures.** Macaulay duration, modified duration, and dollar duration for Bond A and for Bond B (10-year, 4% coupon).
4. **Hedge.** The short position in Bond B is sized so that the dollar durations of the two positions cancel.
5. **Stress test.** 13 parallel yield shocks from -3.00% to +3.00% in 0.5% steps, comparing unhedged and hedged P&L.
6. **Convexity.** Price changes are re-estimated as %ΔP ≈ (-modified duration × Δy) + ½ × convexity × (Δy)², and the hedged P&L is recalculated.

## Limits

- Yields shift in parallel across the curve. Twists and changes in curve shape are not tested.
- Cash flows are fixed, with no default risk, call features, or credit spreads.
- A single hedging bond can match duration but not convexity as well.
- The convexity results are second-order estimates, not full repricing of each bond.

## Files

- `Fixed_Income_Duration_Hedging_Report.pdf`: the full write-up, including the valuation comparison, hedge construction, and conclusions
- `Fixed_Income_Duration_Hedging_Model.xlsx`: the Excel model, with sheets for bond valuation, the duration hedge, the convexity-adjusted hedge, and a side-by-side comparison

This is a learning project and not investment advice.

