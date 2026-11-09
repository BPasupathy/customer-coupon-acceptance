## Live Vercel deployment

[Open the deployed project](https://customer-coupon-acceptance.vercel.app)

# Customer Coupon Acceptance Analysis

An exploratory statistical analysis of the UCI **In-Vehicle Coupon Recommendation** dataset. The objective is to understand which driving, demographic and visit-frequency contexts are associated with coupon acceptance, then translate those findings into practical merchant and mobile-marketing recommendations.

## Repository contents

- [Notebook](notebooks/prompt.ipynb): data validation, cleaning, overall acceptance, Bar and Coffee House segment analysis, hypothesis tests and visualizations.
- [Dataset instructions](data/README.md): reproducible download of the original UCI CSV.
- [Images](images/): charts exported by the notebook when it is run.
- [Requirements](requirements.txt): Python dependencies.

## Dataset

Source: [UCI Machine Learning Repository — In-Vehicle Coupon Recommendation](https://archive.ics.uci.edu/dataset/603/in+vehicle+coupon+recommendation)  
DOI: [10.24432/C5GS4P](https://doi.org/10.24432/C5GS4P)  
License: CC BY 4.0. Cite the UCI dataset when reusing it.

The dataset contains 12,684 survey observations and 25 explanatory variables plus the binary outcome `Y`. The survey describes a driving scenario and whether the respondent would accept a presented coupon.

### Download the data

Run the notebook from the repository root. Its first data-loading cell downloads the official CSV into `data/coupons.csv` if the file is not already present. Alternatively, follow [data/README.md](data/README.md).

## Analysis questions

1. What proportion of all presented coupons were accepted?
2. What is the acceptance rate for Bar coupons?
3. How does Bar coupon acceptance differ for drivers visiting bars at most 3 times per month versus more than 3 times?
4. Among drivers visiting bars more than once per month, how does acceptance vary for age over 25, passenger context and marital status?
5. What happens for the combined segment of frequent bar visitors with no children in the car and a non-farming occupation?
6. Does Coffee House coupon acceptance vary by visit frequency and time of day?

## Methodology and interpretation

- Missingness is inspected before treatment. The high-missingness `car` column is excluded; low-missingness visit-frequency fields are imputed with their modal category, with missingness retained in the audit table.
- Category strings are trimmed and normalized; the source column spelling `passanger` is standardized to `passenger`.
- Segment acceptance is always calculated as accepted coupons divided by coupons offered within that segment. The notebook reports segment sizes alongside rates.
- Two-proportion tests are used for selected independent-group comparisons. These are observational survey associations, not causal effects. Interpret p-values alongside sample sizes and practical differences.
- The dataset has repeated scenario observations from survey respondents; do not treat these results as randomized campaign experiments.

## Running

```bash
python -m pip install -r requirements.txt
jupyter notebook notebooks/prompt.ipynb
```

Run all cells from top to bottom. Charts are saved to `images/`.

## Citation

Wang, T., Rudin, C., Doshi-Velez, F., Liu, Y., Klampfl, E., & MacNeille, P. (2017). A Bayesian framework for learning rule sets for interpretable classification. *Journal of Machine Learning Research*, 18(1), 2357–2393. Dataset: UCI Machine Learning Repository, *In-Vehicle Coupon Recommendation* (2017), DOI: 10.24432/C5GS4P.
