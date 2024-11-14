
# Red-Wine-Quality-Classification

Can we predict the quality of wine based on its physicochemical components?

![w3](https://github.com/user-attachments/assets/6bd61e3c-58a9-436d-92e1-ccf75743d4d3)

## Project Overview

The goal of this project is to predict whether a red wine is of high or low quality based on its chemical properties. We will treat this as a binary classification problem by converting the original quality ratings (scale from 1-10) into two categories: high quality (1) and low quality (0).

## Dataset, Features and Target Variable
This dataset contains physicochemical properties of 1,599 red wine samples from the Vinho Verde region in Portugal. There are 11 input features representing different chemical properties of the wines, and one output variable (quality) based on sensory data.

The dataset includes the following features:

* Fixed acidity - Represents non-volatile acids in wine, primarily tartaric acid.
* Volatile acidity - Measures the amount of acetic acid in wine.
* Citric acid - A weak organic acid naturally present in grapes.
* Residual sugar - The amount of sugar remaining after fermentation stops.
* Chlorides - Represents the amount of salt in the wine.
* Free sulfur dioxide - The free form of SO2 in wine.
* Total sulfur dioxide - The total amount of SO2 in wine (free and bound forms).
* Density - The mass per unit volume of wine.
* pH - Measures the wine's acidity or basicity on a scale of 0-14.
* Sulphates - A wine additive that contributes to SO2 levels.
* Alcohol - The percentage of alcohol by volume in the wine.
* Quality - A sensory score given to the wine on a scale of 0-10.
* Is High Quality (Target variable) - High quality is defined as a quality score of 7 and above (1); otherwise, it is considered low quality (0).

#### **Feature Data Types**
All features in the dataset are recorded as continuous values of type float64, with the exception of the target variable `quality` and the derived `is_high_quality` feature, which are of type int64.

#### **Missing Values**
There are **no missing values** in the **1,599** entries of the dataset.

#### **Target Variable**
The target variable, `quality`, is based on sensory evaluations rated on a scale from 0 to 10. In our dataset, the quality scores range from 3 to 8. We have converted these scores into a binary classification system: scores of 7 and above are classified as high quality (1), while scores below 7 are considered low quality (0). This threshold was selected to balance the number of samples while maintaining a high-quality standard.
