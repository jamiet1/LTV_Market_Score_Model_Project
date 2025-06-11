# Metro LA LTV Market Score Model

## Project Summary

This project calculates a **Market Score** and assigns a **Max Loan-to-Value (LTV)** ratio for each ZIP Code in **Metro Los Angeles**. The goal is to help private lenders assess how much risk is appropriate based on local housing market strength.

Each ZIP code is treated as its own real estate micro-market. We combine **housing data** and **median income estimates** to generate a 0 – 100 Market Score and apply an adjustment framework.

This model is built for **Metro Los Angeles**, covering ZIPs in:
- Los Angeles County  
- Orange County  
- Ventura County  
- Riverside County  
- San Bernardino County

The analysis draws on housing market data spanning from 2017 through 2024, and incorporates median income estimates from the U.S. Census 2023 ACS 5-Year dataset, which reflects income conditions during 2022–2023.

- View the project website here:  https://sites.google.com/g.ucla.edu/ltv-market-score-model-project/home

----

## Preview

<div class='tableauPlaceholder' id='viz1749676077116' style='position: relative'><noscript><a href='#'><img alt='Average Market Score by ZIP Code ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Av&#47;Ave_Score&#47;Sheet1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Ave_Score&#47;Sheet1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Av&#47;Ave_Score&#47;Sheet1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>    

<div class='tableauPlaceholder' id='viz1749675831579' style='position: relative'><noscript><a href='#'><img alt='Max LTV by ZIP Code ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ma&#47;Max_LTV&#47;Sheet2&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Max_LTV&#47;Sheet2' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ma&#47;Max_LTV&#47;Sheet2&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>

----

## Original Data Sources

1. **Redfin ZIP Code Market Tracker**  
   - URL: [Redfin ZIP Market Tracker](https://redfin-public-data.s3.us-west-2.amazonaws.com/redfin_market_tracker/zip_code_market_tracker.tsv000.gz)  
   - Variables used: median sale price, days on market, homes sold, sale-to-list ratio

2. **Census Median Income Data**  
   - URL: [Census Table B06011](https://data.census.gov/table/ACSDT5Y2023.B06011?q=B06011:+Median+Income+in+the+Past+12+Months+(in+2023+Inflation-Adjusted+Dollars)+by+Place+of+Birth+in+the+United+States&g=040XX00US06$8600000)  
   - Used for: Median household income by ZIP

----

## Methodology

### Market Score on a 0 – 100 scale

Each ZIP code gets a score based on:
- **Sale-to-List Ratio**: How close homes sell to asking price
- **Homes Sold**: Volume of completed transactions
- **Days on Market (DOM)**: Speed at which homes sell
- **Median Income**: Local economic strength

These metrics are ranked across ZIPs and combined with the following weights:
- 35% Sale-to-List Ratio  
- 35% Homes Sold  
- 15% Speed of Sale (DOM)  
- 15% Median Income  

### LTV Adjustment Framework

  Level | Factor                     | Impact
|-------|----------------------------|----------------------------|
| 1     | **County-level risk**      | ±0–2%                      |
| 2     | **Market Score category**  | Prime: +2%, Declining: -5% |

- Final LTV is capped between **60% and 75%**
- Default base LTV is **70%**

----

## Output

- ZIP-level table of:  
  - Market Score  
  - Market Category (Prime / Neutral / Declining)  
  - Max LTV  
  - Median Income  
- Visualizations of score distribution, LTV vs. score, income vs. score, etc.
- Exported CSV **Metro_LA_LTV_Scores.csv** for further use
