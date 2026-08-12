# Fixed Income Valuation, Duration Hedging & Convexity

An Excel-based fixed-income model covering bond valuation, interest-rate sensitivity, and hedge performance. Prices a bond under both a flat-yield method and a term-structure method using real U.S. Treasury yield data (FRED), then builds a duration-matched hedge and extends the analysis through convexity.

The duration hedge held portfolio P&L within $0.02 across yield shocks of ±3%. Extending the analysis with convexity reveals the residual nonlinear exposure that a duration-only hedge misses.

## Files
- `Fixed_Income_Duration_Hedging_Report.pdf` — full write-up: methodology, valuation comparison, duration hedge, convexity-adjusted results, and conclusion
- `Fixed_Income_Duration_Hedging_Model.xlsx` — the Excel model: bond pricing, duration/convexity calculations, hedge construction, and yield-shock scenario analysis

