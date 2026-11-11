# Sleep Duration and Poor Mental Health Days: BRFSS 2013

An exploratory analysis in R of whether the number of hours a person sleeps is associated with the number of days they report poor mental health, using the CDC's 2013 Behavioral Risk Factor Surveillance System (BRFSS) survey.

**Full report:** [Full Analysis](https://tonet21.github.io/brfss-sleep-mental-health-r/Analysis.html)

## Research question

Is there an association between sleep duration and the number of days of poor mental health reported?

## Data

- **Source:** [Behavioral Risk Factor Surveillance System, 2013](https://www.cdc.gov/brfss/annual_data/annual_2013.html), CDC.
- **Collection:** annual telephone survey (landline and mobile) of US adults, run by each state using a core set of standardized questions from the CDC.
- **Variables used:**
  - `sleptim1`: hours of sleep in a 24-hour period
  - `menthlth`: number of days in the past 30 with poor mental health
  - `sex`: used to split the comparison
- **Note:** the dataset (~55 MB) is **not included** in this repository because of its size. See "How to reproduce" below.

## Methods

1. **Data quality checks:** calculated the share of missing values in the three variables (all under 5%, so rows with missing values were dropped) and checked for the non-valid codes 77 and 99, which were not present in this version of the data.
2. **Recoding:** `menthlth` value 88 (meaning "none") was recoded to 0.
3. **Sleep categories:** hours of sleep were grouped into three categories: under 6, 6 to 8, and over 8 hours. Group choice was based on common recommendations in the sleep literature and checked against the distribution in a histogram.
4. **Outcome choice:** `menthlth` is heavily right-skewed and its median was 0 in every group, so the median was uninformative. Instead, I compared the **percentage of people reporting at least one poor mental health day** in each sleep category, split by sex.
5. **Visualization:** grouped bar chart built with `ggplot2`.
6. **Sampling review:** a written assessment of how the survey design (telephone sampling, state-run collection, stratified sampling) could introduce bias.

## Key findings

- People sleeping **6 to 8 hours** reported poor mental health days least often.
- The **over 8 hours** group looked similar to the 6 to 8 hour group.
- People sleeping **under 6 hours** had the highest share reporting poor mental health days.
- **Women** reported poor mental health days more often than men across all sleep categories.

## Limitations

- This is an **observational** survey, so the results show an association, not causation. Poor mental health can also disrupt sleep, so the direction of the relationship cannot be determined from this analysis.
- Sleep and mental health are **self-reported** and may be inaccurate.
- The analysis is **descriptive only**: no confounders (age, income, physical health) were controlled for, and no statistical tests or models were applied.
- Telephone surveys can under-represent people without phones or with limited availability.
- BRFSS sampling weights were not applied, so the results describe the respondents rather than the whole US population.

## How to reproduce

**Requirements:** R, RStudio, and the packages `ggplot2` and `dplyr`.

```r
install.packages(c("ggplot2", "dplyr"))
```

1. Clone or download this repository.
2. Get the BRFSS 2013 dataset (`brfss2013.RData`) from the source above and place it in the **same folder** as `Analysis.Rmd`.
3. Open `Analysis.Rmd` in RStudio and click **Knit**.
