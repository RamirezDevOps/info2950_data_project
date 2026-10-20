# Preregistration of analyses

Copied from the updated [Phase II notebook](<Phase II.ipynb>); also included in the [PDF report](<Phase II.pdf>).

##### Hypothesis 1:
**Months in which Biden’s approval rating was lower will have a higher share of political podcast episodes mentioning him**, after accounting for the time trend over his presidency.

##### Analysis:
We understand from politcal science that controversy or disapproval of a subject often results in it being more covered by the media. To see if this applies in our data, we will run a **multivariable linear regression** where the outcome is the **monthly mention rate** and the explanatory variables are **monthly approval rating and a month counter (1 to 47)** to account for changes over his presidency. We will use ordinary least squares and **test whether β_approval < 0, using a one-tailed t-test at α = 0.05**. (A significantly negative β_approval would mean that lower approval is associated with a higher mention rate.) Also, because consecutive months can be correlated with one another, we will **check the residuals for indications of dependence on time** and note oddities in our limitations. We will report the result regardless of statistical significance. December 2022 will be excluded because it has no approval rating.

##### Hypothesis 2:
**The relationship between Biden's approval rating and his mention rate differs between conservative and liberal podcasts.**

##### Analysis:
We understand from political science that politcal polarization in the United States can result in media coverage of certain issues to differ from one another based on ideological tendency. To see if this applies to our data, we will run a **multivariable linear regression** where the outcome is **`Liberal_Conservative_Difference`** and the explanatory variables are **monthly approval rating and a month counter (numbered 1 to 47 across all months)** to account for changes over Biden's presidency. Because the outcome is the liberal rate minus the conservative rate, **β_approval equals the difference between the two groups' approval slopes**. We will use ordinary least squares and **test whether β_approval ≠ 0 using a two-tailed t-test at α = 0.05**. (A significant β_approval would mean that the relationship between approval and mention rates differs between conservative and liberal podcasts.) Because consecutive months can be correlated, we will **check the residuals for dependence over time** and discuss any concern in our limitations. We will report the result regardless of statistical significance. December 2022 will be excluded because it has no approval rating.

### Questions for reviewers

* For our hypotheses, **is a linear month counter enough to account for changes over his presidency, or should we use something else that handles time better?** Additionally, how significant is it that a large part of the variation in approval comes from the first year?

* In our data, the overall mention proportion peaks at about 0.40 in July 2024 and then falls to roughly 0.11–0.16, and this spike appears in all three political leanings. This is also when Biden withdrew and approval rose from 0.36 to 0.43. For our regressions, **how should we deal with these abnormal months?** Should we keep everything as is, exclude those months, add a dummy variable for the withdrawal period, or do something else? **What are the benefits and costs of these options?**

* We are concerned about whether or not we can derive any significant conclusions from podcast data that falls in the moderate category. For context, the moderate category contains only 9 shows and 3,897 episodes (about 80 per month), compared with 43 conservative shows and 44 liberal shows. **Is this too small to learn anything reliable about moderate podcasts, or can we include them in our analysis if we describe the limitations?** If not, how should we incorporate moderate podcasts into our analysis if at all?
