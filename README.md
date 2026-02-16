# British Airways Lounge Demand Estimation

This project builds an operationally scalable framework to estimate airport lounge demand based on flight schedules, passenger tiers, and travel patterns.

## Business Problem

British Airways requires a method to forecast lounge eligibility across changing flight schedules at Heathrow Terminal 3. The solution must remain robust even when flight numbers, fleet mix, and destinations change.

## Approach

- Data auditing and validation
- Feature engineering (total seat capacity)
- Testing multiple grouping strategies
- Comparing segmentation variance
- Selecting optimal grouping based on operational simplicity and explanatory power
- Building a reusable lookup table

## Key Findings

- Time of Day alone provides weak segmentation.
- Haul (Long vs Short) introduces meaningful differentiation.
- The combination of Haul × Time of Day delivers strong variance in Tier 3 demand while remaining operationally simple.
- Arrival Region adds complexity without significant predictive benefit.

## Outcome

A reusable lookup framework using 8 segments (Haul × Time of Day) that can be applied to future schedule forecasts without relying on flight-level memorisation.

## Tools Used

- Python
- Pandas
- NumPy
- Excel
