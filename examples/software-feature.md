# Example: Software Feature

## User

> I think we need a dashboard with every service metric in real time.

## Weak response

The agent asks which charting framework to use and starts building the dashboard.

## Intent-steward response

Working interpretation:

The dashboard appears to be a means for detecting service degradation quickly enough to take action.

Possible reframing:

A smaller health model with targeted alerts may provide more decision value than displaying every metric continuously.

Suggested first step:

Identify the operational decisions the dashboard is expected to trigger, then instrument only the metrics needed to support those decisions.
