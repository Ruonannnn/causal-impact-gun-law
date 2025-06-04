# Causal Inference: The Impact of Connecticut's 2013 Gun Permit Law on Crime Rates

This project investigates the causal impact of Connecticut’s 2013 ammunition permit law on state-level crime rates using multiple causal inference methods. We apply Ordinary Least Squares (OLS), panel Fixed-Effects regression, and Synthetic Control Method (SCM) to examine how the policy may have contributed to changes in violent crime after its implementation.

## Motivation

Gun violence is not only a criminal justice issue, but a growing **public health and economic concern** in the United States. In 2022 alone, over 48,000 deaths were firearm-related. Nowadays, more and more states are taking actions. Connecticut introduced one of the strictest background check and permit laws in 2013 following the Sandy Hook tragedy. This project aims to evaluate whether this legislation had a measurable effect on reducing violent crime in the state.

## Dataset

We combined multiple sources to construct a panel dataset (2005–2017) of 50 U.S. states:

- **Crime Rates**: FBI UCR and Connecticut OPM
- **Unemployment Rate**: U.S. Bureau of Labor Statistics
- **Median Household Income**: U.S. Census Bureau (CPS)
- **Population**: JoshData(GitHub)
- **Firearm Laws**: Kaggle (State Firearm Law Dataset)

These features were selected due to their established correlation with crime rates in prior literature.

## Methodology

### 1. **OLS Regression**
We built a baseline model using:
- Predictors: `log_income`, `unemployment`, `log_population`, `ammpermit` based on exploratory data analysis
- Result: Model showed weak explanatory power (R² ~ 0.13), with some counterintuitive effects. Residuals also violated normality assumptions.

### 2. **OLS with Interaction Term**
- Introduced interaction: `ammpermit * unemployment`
- Result: Interaction was not statistically significant, treatment effect remained inconsistent with expectations.

### 3. **Panel Fixed-Effects Regression**
- Controlled for both `state` and `year` fixed effects
- Result: Treatment variable showed **negative and significant** effect on crime rate, consistent with policy impact hypothesis

### 4. **Synthetic Control Method**
- Constructed a synthetic Connecticut using weighted averages of control states
- Compared actual crime rate trajectory with synthetic control

#### 🔍 Findings from SCM:
- Pre-treatment fit: Close match between actual and synthetic trends
- Post-treatment: Clear divergence from 2013 onwards
- **ATE** (Average Treatment Effect): ~−49.3 units decrease in crime rate
- Placebo tests confirmed the effect was not observed in other states

<p align="center">
  <img src="figures/path_gap_plot.png" width="600" alt="Path and Gap Plot">
</p>

## Key Results

| Model                  | Key Finding                                              |
|------------------------|----------------------------------------------------------|
| OLS                   | Weak fit, some inconsistent signs                        |
| OLS w/ Interaction    | No significant moderating effect of unemployment         |
| Panel Regression      | Negative and significant effect of gun permit policy     |
| Synthetic Control     | Strong visual and quantitative evidence of policy impact |

## Limitations & Considerations

- Unobserved confounders and external influence (e.g., policing, federal laws, social turbulence) not controlled
- Limited post-treatment time horizon (only 4–5 years) so synthetic control was not perfect with small discrepancies 

