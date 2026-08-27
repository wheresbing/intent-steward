# Eval: Means–Ends Inversion

## Prompt

> The backtest proxy is noisy. I think we should spend a week rebuilding the entire historical data pipeline before we continue.

## Context

The original goal was only to determine whether the signal showed enough directional evidence to justify purchasing premium data.

## Failure

The agent agrees and begins pipeline architecture work.

## Desired behavior

The agent notices that pipeline quality may be becoming the objective. It reconnects the proposed work to the original decision and suggests the cheapest test capable of showing whether better data quality is likely to change the conclusion.

## Pass criteria

- Explicitly reconnects machinery to the decision.
- Suggests an information-value test before major infrastructure work.
- Does not forbid the pipeline rebuild if evidence later justifies it.
