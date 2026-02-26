# British Airways Lounge Demand Estimation

## Business Problem

Airport lounges operate with fixed capacity but variable passenger demand depending on flight schedules, passenger tiers, and travel patterns. British Airways requires a scalable method to estimate future lounge demand in order to optimise staffing, space allocation, and operational planning.

However, flight schedules change frequently due to route adjustments, aircraft allocation, and seasonal variation. A reliable prediction approach must therefore use stable, reusable flight characteristics rather than relying on individual flight numbers.

This project develops a data-driven lookup model to estimate lounge-eligible passenger demand based on flight characteristics such as haul length and time of departure.

The objective is to identify grouping strategies that balance predictive accuracy with operational simplicity, allowing the model to generalise to future flight schedules.

---

## Dataset

The dataset contains British Airways flight schedule data with:

- 10,000 flight records  
- 17 variables describing flight timing, route, aircraft, and passenger eligibility  
- Passenger eligibility counts across three lounge-eligible tiers  

### Key predictor variables

Flight characteristics:

- Haul length (Short-haul vs Long-haul)  
- Time of day (Morning, Lunchtime, Afternoon, Evening)  
- Arrival region (Europe, North America, Asia, Middle East)  

Aircraft and capacity variables:

- First class seats  
- Business class seats  
- Economy seats  

Passenger eligibility variables:

- Tier 1 eligible passengers  
- Tier 2 eligible passengers  
- Tier 3 eligible passengers  

### Engineered features

Total passenger capacity per flight:

TOTAL_SEATS = First Class + Business Class + Economy Seats

This enables calculation of lounge eligibility rates as a percentage of total capacity.

---

## Approach

### Data Preparation

- Loaded and audited dataset structure and completeness  
- Validated categorical variables and group distributions  
- Confirmed absence of missing values  
- Verified passenger eligibility and seat capacity variables  

### Feature Engineering

Created new analytical variables to support lounge demand estimation:

- Total seats per flight  
- Total eligible passengers per flight  
- Eligibility percentages relative to seat capacity  

These features allow comparison of lounge demand across flight groupings.

### Grouping Strategy Evaluation

Multiple grouping strategies were tested to determine which best explains variation in lounge demand:

- Haul length  
- Time of day  
- Arrival region  
- Haul × Time of day  
- Haul × Arrival region  
- Time of day × Arrival region  
- Haul × Time of day × Arrival region  

Each grouping was evaluated based on percentage-point variation in lounge eligibility rates.

Higher variation indicates stronger predictive usefulness.

### Model Selection

The optimal grouping was identified as:

Haul × Time of Day

This grouping was selected because it:

- Provides strong differentiation in eligibility rates  
- Maintains operational simplicity with only 8 segments  
- Avoids excessive fragmentation from overly complex groupings  

### Lookup Table Construction

A reusable lookup table was created containing:

- Number of flights per segment  
- Total seat capacity per segment  
- Tier-specific lounge eligibility percentages  

This lookup table enables scalable estimation of lounge demand for future schedules.

---

## Results

The final lookup table identified clear structural differences in lounge demand across flight segments.

Key findings include:

Short-haul flights:

- Tier 3 eligibility rates range from approximately 16.6% to 17.3%  
- Higher eligibility rates compared to long-haul flights  

Long-haul flights:

- Tier 3 eligibility rates range from approximately 10.3% to 10.6%  
- Lower overall eligibility rates but larger absolute passenger volumes  

Time-of-day variation also influences lounge demand, though haul length is the dominant driver.

The final model provides a simple and scalable framework for predicting lounge demand across future schedules.

---

## Key Findings

The strongest predictors of lounge demand were:

- Haul length (Short-haul vs Long-haul)  
- Time of departure  

Arrival region provided only marginal improvement while significantly increasing model complexity.

Short-haul flights consistently showed higher lounge eligibility rates relative to total seat capacity.

Long-haul flights generate larger absolute lounge volumes but lower proportional eligibility rates.

The final Haul × Time of Day grouping balances predictive accuracy and operational usability.

This approach enables British Airways to estimate lounge demand even when full flight-level detail is unavailable.

---

## Tech Stack

Python  
pandas  
numpy  

### Analytical Techniques

- Exploratory data analysis  
- Feature engineering  
- Group-based aggregation modelling  
- Lookup table construction  
- Operational demand modelling  

---

## How to Run

### Clone repository

```bash
git clone https://github.com/hayleymer/ba-lounge-demand-estimation.git
```

### Navigate to project folder

```bash
cd ba-lounge-demand-estimation
```

### Install dependencies

```bash
pip install -r requirements.txt
```

Run the notebook to reproduce the analysis and lookup table.
