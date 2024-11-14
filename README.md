
# Red-Wine-Quality-Classification

Can we predict the quality of wine based on its physicochemical components?

![w3](https://github.com/user-attachments/assets/6bd61e3c-58a9-436d-92e1-ccf75743d4d3)

## Project Overview

The goal of this project is to predict whether a red wine is of high or low quality based on its chemical properties. We will treat this as a binary classification problem by converting the original quality ratings (scale from 1-10) into two categories: high quality (1) and low quality (0).

## Dataset, Features and Target Variable
This dataset contains physicochemical properties of 1,599 red wine samples from the Vinho Verde region in Portugal. There are 11 input features representing different chemical properties of the wines, and one output variable (quality) based on sensory data.

The dataset includes the following features:

* `Fixed acidity` - Represents non-volatile acids in wine, primarily tartaric acid.
* `Volatile acidity` - Measures the amount of acetic acid in wine.
* `Citric acid` - A weak organic acid naturally present in grapes.
* `Residual sugar` - The amount of sugar remaining after fermentation stops.
* `Chlorides` - Represents the amount of salt in the wine.
* `Free sulfur dioxide` - The free form of SO2 in wine.
* `Total sulfur dioxide` - The total amount of SO2 in wine (free and bound forms).
* `Density` - The mass per unit volume of wine.
* `pH` - Measures the wine's acidity or basicity on a scale of 0-14.
* `Sulphates` - A wine additive that contributes to SO2 levels.
* `Alcohol` - The percentage of alcohol by volume in the wine.
* `Quality` - A sensory score given to the wine on a scale of 0-10.
* `Is High Quality` (Target variable) - High quality is defined as a quality score of 7 and above (1); otherwise, it is considered low quality (0).

#### **Feature Data Types**
All features in the dataset are recorded as continuous values of type float64, with the exception of the target variable `quality` and the derived `is_high_quality` feature, which are of type int64.

#### **Missing Values**
There are **no missing values** in the **1,599** entries of the dataset.

## **Target Variable**
The target variable, `quality`, is based on sensory evaluations rated on a scale from 0 to 10. In our dataset, the quality scores range from 3 to 8. We have converted these scores into a binary classification system: scores of 7 and above are classified as high quality (1), while scores below 7 are considered low quality (0). This threshold was selected to balance the number of samples while maintaining a high-quality standard.

Distribution of Quality Scores
![image](https://github.com/user-attachments/assets/835a7604-d429-49c2-9318-ed3cf3647b75)

## **Imbalance Data**
Our dataset shows a substantial imbalance between high and low-quality wines, with high-quality wines accounting for approximately 14% of the samples.

Distribution of Target Value
![image](https://github.com/user-attachments/assets/63076004-a762-4c2e-bb43-0855fafbf30a)


## **Data Preprocessing**
To enhance our model's predictive power, we applied advanced feature transformations (log, square root, Yeo-Johnson) and used the SelectKBest method for feature selection. This process led to a new 'Transformed Data' dataset with optimally processed features.

**Key Outcomes:**
* Outlier Reduction: Reduced total outliers from 573 to 315 (45% reduction).
* Outlier Percentage: Decreased from 35.83% to 19.70%.
* Features without Outliers: Six features now have no outliers after transformation.

Here is an example of how this transformation affected the distribution and outliers reduction of fixed acidity

**Original Data**

![image](https://github.com/user-attachments/assets/b9807594-df2d-4ef0-b587-c1e419eae7a5)

**Transformed Data**

![image](https://github.com/user-attachments/assets/aee37cc9-f4a7-4fd7-974d-800afc8f90f4)


## **Correlation Analysis & Feature Importance**
**Feature transformations enhanced correlations with the target column:**
* Sulphates correlation increased from 0.199 to 0.283
* Residual sugar slightly improved from 0.048 to 0.064
* Negative correlations strengthened for volatile acidity and total sulfur dioxide
  
![image](https://github.com/user-attachments/assets/79ffb72c-1241-4700-bf77-40ae0f4e518d)


  
**Feature importance (SelectKBest scores) showed:**
* Alcohol remained the most significant feature (score: 317.65)
* Volatile acidity increased from 126.29 to 147.45
* Sulphates increased from 66.19 to 139.53

 ![image](https://github.com/user-attachments/assets/0144aff1-edd9-4fdc-9c51-ad0f850731f5)  ![image](https://github.com/user-attachments/assets/fe64084c-89e3-4040-8e43-08c9c5c44635)  ![image](https://github.com/user-attachments/assets/0614ac4c-12b3-4e51-b692-51e92d325122)





## **Methodology**
We chose the F1 score as our primary evaluation metric for the following reasons:
* **Balance between Precision and Recall**: The F1 score provides a balanced measure of both precision and recall, which is crucial in our case where we want to accurately identify high-quality wines without missing too many or incorrectly classifying low-quality wines.
* **Class Imbalance**: Our dataset has a significant imbalance between high and low-quality wines, with high-quality wines (rated 7 and above) representing only about 14% of the samples. The F1 score is particularly useful in such imbalanced scenarios as it takes both false positives and false negatives into account, providing a more reliable performance measure than accuracy alone.
* **Note**: We also explored the use of F-beta scores, specifically with beta values of 1.2 and 1.5, to potentially give more weight to recall. However, our analysis revealed an interesting pattern: For these beta values, we consistently observed few true positive predictions and at least three times as many false negative predictions. This imbalance persisted across different beta values, indicating a potential bias in our model towards negative predictions. Given these observations, we decided to stay with the F1 score as our primary evaluation

### **Model Performance Progression**
Our model's performance improved significantly through various stages:
* Initial Logistic Regression: F1 score 0.3478.
  ![image](https://github.com/user-attachments/assets/a9b5366a-927b-45d4-bbd8-0d9b26672448)

* After feature transformation: F1 score 0.4314.
  ![image](https://github.com/user-attachments/assets/95df3ef2-fd25-4af7-9af2-7c52e6f362b9)

* With oversampling (75%): F1 score 0.5618.
![image](https://github.com/user-attachments/assets/0604eb6b-33ac-4817-b2f8-cc5a8e99f60c)
![image](https://github.com/user-attachments/assets/334e480a-ea2d-43cb-b5ac-dc97eaaa01dc)

* After Optuna optimization: F1 score 0.6104.
![image](https://github.com/user-attachments/assets/73993f84-4d37-4872-9796-e976d4e340b4)


## **Cross Validation & Model Performance Analysis**
We conducted a 40-fold cross-validation, revealing high variability in model performance (mean F1 score: 0.521). 

![image](https://github.com/user-attachments/assets/55dc718e-5750-4416-91ac-a221025e3e4f)

The model performed reliably with extreme scores but struggled with mid-range scores.

![image](https://github.com/user-attachments/assets/a7dcbff8-f760-4b61-8792-342eae5f0741)


![image](https://github.com/user-attachments/assets/ee0bd82d-359f-4341-8bf7-706bfb010c25)


## **Multi Classifier Optimization & Ensemble Models**
We optimized six classifiers using Optuna. LightGBM emerged as the best individual model with an F1 score of 0.633 and accuracy of 0.908. However, our final ensemble model (combining Logistic Regression, KNN, and LightGBM) achieved the highest F1 score of 0.6812 with an accuracy of 0.908.

![image](https://github.com/user-attachments/assets/bb24386f-1b1c-4a40-acf2-fcef4924f711)


## **Key Findings & Conclusions**

**Conclusions:**

* Feature Engineering: The transformation of features significantly reduced outliers and improved model performance, highlighting the importance of proper data preprocessing.
* Imbalanced Data Handling: Oversampling, especially with optimized strategies, proved crucial in addressing the class imbalance issue.
* Model Selection: While individual models like LightGBM performed well, the ensemble approach provided the best balance of precision and recall.
* Performance Metrics: The F1 score was an effective metric for this imbalanced dataset, providing a balanced measure of model performance.
* Challenges in Mid-range Predictions: The models struggled with wines rated 6-7, suggesting a need for further investigation into these borderline cases.
* Consistency vs. Performance: Some models (like KNN) showed high consistency but lower overall performance, while others (like XGBoost) showed higher but more variable performance.

**Future Work**

Due to time constraints, several aspects could be further examined:

* Correlated Features: Investigate the impact of dropping highly correlated features on model performance.
* Mid-range Scores: Focus on improving classification for wines rated 6-7, possibly by adjusting the threshold or developing a more nuanced scoring system.
* Feature Importance: Conduct a deeper analysis of feature importance across different models to identify key predictors of wine quality.
* Hyperparameter Tuning: Further optimize model parameters, especially for the ensemble model.

**We hope you found this journey through data preprocessing, model optimization, and ensemble creation as enlightening as we did! 
See you at our next project—cheers!** 🍷
