# Supply Chain Performance Analysis

Capstone project for the Professional Certificate Programme in Data Science for Business Decisions, IIM Kozhikode (DSBD-02).

Analysis of a 100-SKU supply chain dataset in R. Products are skincare, haircare and cosmetics. The goal was to answer ten business questions about revenue, suppliers, shipping, inventory and product performance.

Group 8: Santosh Birajdar, Nalini S, Surbhi, Shreedhar S R.

## Questions and methods

1. Which product categories make the most revenue — grouped summary
2. Do suppliers differ in lead time — one-way ANOVA, then Tukey HSD
3. What drives revenue — multiple linear regression, VIF check for multicollinearity
4. Which shipping carrier is best on cost vs speed — cost per day of speed
5. What do defects cost — regression coefficient applied across SKUs
6. Economies of scale in production — correlation and linear model
7. Is stock matched to sales — stock-to-sales ratio by category
8. Product segments — K-means on scaled data, elbow method to pick k
9. Can high performers be predicted — Random Forest, 80/20 split, 5-fold CV
10. Which product attributes matter most — feature importance

## Results

- Skincare is the biggest category: $1.06M, 46% of total revenue
- Supplier lead times are significantly different (p < 0.01), from 11.67 to 20.40 days
- Units sold is the strongest revenue predictor: +$38.14 per unit (p < 0.001). Average price is $49.46, so the coefficient is in a sensible range
- Defect rate: -$5,640 revenue per 1% increase (p < 0.001)
- Manufacturing cost, lead time and production volume were not significant
- Random Forest: 95% accuracy on the test set, sensitivity 0.90, specificity 1.00

## Notes on the model

The target is whether a SKU is above or below median revenue. So `revenue_generated` is left out of the predictors. If it were included the model would score near 100% and the result would be meaningless. Predictors used: price, units sold, manufacturing cost, lead time, defect rate.

Units sold comes out as the top predictor, but revenue is roughly price times units, so some of that is arithmetic rather than a finding. The defect rate result is the more useful one because it is not built into the target.

## Limitations

- 100 SKUs is a small sample
- Single time period, so no trends
- Revenue only, no margin data
- Market and competitor effects not in the data

## How to run

```r
install.packages(c("tidyverse", "janitor", "corrplot", "randomForest",
                   "caret", "knitr", "car", "broom", "factoextra"))
```

Put `supply_chain_data.csv` in the same folder and knit `Supply_Chain_Analysis_Complete.Rmd`. The data file is not in this repo.

## Files

- `Supply_Chain_Analysis_Complete.Rmd` — the analysis, all ten questions
- `Supply_Chain_Analysis_Complete.html` — the knitted report, viewable in a browser without R
