Student Performance Prediction

An R-based statistical modelling project that investigates the factors associated with secondary-school students' final mathematics grades. The project uses exploratory data analysis, multiple linear regression, diagnostic testing, transformations, multicollinearity treatment, stepwise selection, cross-validation, and a complementary logistic model.

Project overview

The analysis uses the mathematics subset of the UCI Student Performance dataset:

395 students

33 variables

16 numerical variables and 17 categorical variables

Target variable: G3, the final mathematics grade on a 0–20 scale

The central research question is:

Which academic, demographic, family, and lifestyle factors are most strongly associated with students' final mathematics performance?

Analysis workflow

Load and inspect the student mathematics dataset.

Explore the distribution of grades, absences, failures, and family-related variables.

Screen candidate predictors using correlation analysis, ANOVA, and domain knowledge.

Fit an initial multiple linear regression model.

Inspect residual diagnostics for linearity, homoscedasticity, and normality.

Apply a square-root transformation to G3.

Diagnose multicollinearity between G1 and G2.

Replace G1 and G2 with their average to create a more interpretable prior-performance measure.

Apply backward stepwise selection using AIC.

Compare candidate models using cross-validation.

Fit a logistic regression model for pass/fail classification as a complementary analysis.

Main findings

Earlier academic performance is the strongest predictor of final mathematics performance.

G1 and G2 are highly correlated, so the selected model combines them as (G1 + G2) / 2 to reduce multicollinearity.

The selected linear model explains approximately 62% of the variance in final grades while remaining relatively interpretable.

Family relationships, absences, age, failures, romantic status, alcohol consumption, and extracurricular activities provide smaller additional effects.

The original high-fitting model explains more variance, but its residual diagnostics show non-normality and heteroscedasticity.

A complementary logistic model is used to examine the probability of achieving a passing grade.

Repository structure

Student-Performance-Prediction/
├── student/                    # Student performance datasets and data documentation
├── phtot/                      # Figures used in the presentation files
├── report photo/               # Figures used in the written report
├── report.Rmd                  # Main written project report
├── 4final.qmd                  # Final Quarto reveal.js presentation
├── 3final.qmd                  # Earlier presentation version
├── final_version.rmd           # Model-development notebook
├── normal_model.Rmd            # Regression diagnostics and transformations
├── data_transformation.rmd     # Feature transformations and recoding
├── version_with_outliers.rmd   # Alternative analysis retaining outliers
├── A2.rmd                      # Additional modelling work
└── L04G06.Rproj                # RStudio project file

Requirements

R 4.2 or newer

RStudio is recommended

Quarto is required to render the .qmd presentation

A LaTeX distribution with XeLaTeX is required to render the pinp PDF report

Install the main R packages:

install.packages(c(
  "tidyverse",
  "ggplot2",
  "ggfortify",
  "performance",
  "caret",
  "MASS",
  "knitr",
  "rmarkdown",
  "pinp"
))

Some exploratory files may use additional packages. Install any package named in an R error message before rendering that file.

Getting started

Clone the repository and open the RStudio project:

git clone https://github.com/Denghj-jack/Student-Performance-Prediction.git
cd Student-Performance-Prediction

Then open L04G06.Rproj in RStudio.

Render the main written report:

rmarkdown::render("report.Rmd")

Render the final presentation:

quarto render 4final.qmd

For a code-first view of the modelling process, run the chunks in final_version.rmd or normal_model.Rmd from top to bottom.

Selected model

The final report selects a transformed multiple linear regression model of the general form:

sqrt(G3) ~ prior_grade_average + academic + demographic + family + lifestyle factors

where:

prior_grade_average = (G1 + G2) / 2

This specification was selected because it reduces multicollinearity and offers a practical balance among predictive accuracy, robustness, and interpretability.

Limitations

G3 contains a concentration of low and zero values, which makes standard linear-model assumptions difficult to satisfy.

Earlier grades dominate the prediction, so the model may be less useful when G1 and G2 are unavailable.

The data contains limited psychological, motivational, teaching-quality, and classroom-interaction variables.

The analysis is observational and should not be interpreted as proving causal relationships.

The dataset represents students from Portuguese secondary schools and may not generalise to other education systems.

Possible improvements

Use a reproducible train/validation/test split shared across every model.

Compare regularised regression, random forests, gradient boosting, and ordinal regression.

Report RMSE, MAE, calibration, and confidence intervals consistently.

Add an automated data-processing and model-training script.

Use renv to lock package versions.

Add a data dictionary and a single canonical analysis notebook.

Authors

Hongjie Deng, Anan Wang, Yi Wang, Ranran Zhang, and Jingyi WuThe University of Sydney

Data source

UCI Machine Learning Repository — Student Performance dataset.
