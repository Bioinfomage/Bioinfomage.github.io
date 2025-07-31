---
title: "How I Built a Predictor Model – AutoStack360"
date: 2025-07-31 00:00:00 +0800
categories: [Data_Analysis]
tags: [Data_analysis, Random_Forest_Model, Data_wrangling]
---

# Salary Predictor-Autostack360

📂 GitHub Repository: https://github.com/Bioinfomage/Autostack360


-Introduction-

This project explores how various factors such as professional experience, country, education level, and programming language usage influence developer salaries. The dataset used is the 2024 Stack Overflow Developer Survey. The final goal was to train and evaluate a predictive model that estimates developer salary (log-transformed) from these variables.

-Data Collection & Cleaning-

The raw dataset was collected from the 2024 Stack Overflow Developer Survey. It originally had over 60,000 entries and more than 100 columns. I focused only on professional developers and removed entries with missing salary data, leaving us with approximately 20,000 records.
I cleaned the dataset by dropping columns with excessive missing values or irrelevant content (like AI opinions, news consumption, survey ease etc.). Then, I trimmed the dataset to 84 meaningful columns.

-Exploratory Data Analysis (EDA)-

I applied log transformation on the 'ConvertedCompYearly' salary field to normalize the right-skewed distribution. Also, I filtered out the top 1% and bottom 5% salaries to remove outliers.
Professional experience ('YearsCodePro') was mapped numerically, e.g., 'Less than 1 year' → 0, 'More than 50 years' → 51. I observed a saturation in salary growth beyond ~15 years of experience.
Country was target-encoded using a leakage-free K-Fold approach, capturing average salary trends while avoiding data leakage.
Education levels were simplified into 8 categories and one-hot encoded. Higher education levels like 'Master’s' and 'Professional' correlated positively with salary.
Programming languages (multi-label column) were split using ';' and binarized. Top correlated languages with salary were Bash/Shell, Go, and Rust. Interestingly, Java and JavaScript showed a slightly negative correlation, possibly due to widespread usage among lower/mid-level devs.

-Model Building-

I evaluated three models:
- Linear Regression (RMSE: 0.619, R²: 0.530)
- Ridge Regression (RMSE: 0.610, R²: 0.541)
- Random Forest Regressor (RMSE: 0.585, R²: 0.576)

Random Forest performed the best, thanks to its ability to model non-linear relationships, handle outliers, and capture feature interactions.

-Final Outputs & Deployment-

The final model and outputs include:
- `survey_with_language_nd_Edlevel_binaries.csv`: Preprocessed dataset
- `salary_predictions_random_forest.csv`: Predictions
- `reduced_random_forest_salary_model.pkl`: Trained model

The entire pipeline is ready for deployment and automation using tools like Azure ML, GitHub Actions, and Power BI for visualization.
