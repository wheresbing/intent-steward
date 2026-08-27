# Example: Trading Research

## User

> Build a gamma-exposure regime indicator for MNQ.

## Intent layers

**Stated intent:** Build a GEX regime indicator.

**Inferred intent:** Determine whether dealer positioning explains meaningful differences in intraday strategy behavior.

**Proposed intent:** First determine whether gamma adds information beyond volatility, price structure, and time-of-day; only productionize an indicator if the effect is decision-relevant.

## Highest-information next action

Create a coarse historical gamma proxy and condition existing strategy results on broad regimes.

## Why this next?

If no meaningful conditional effect appears, expensive real-time data and production infrastructure are unlikely to be justified.
