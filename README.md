# Calorie Counter
by Jamila Nagarwala and Mehek Gupta 
jnagar@umich.edu and mehekgup@umich.edu

---

## Introduction

This project analyzes the ‘Recipes and Ratings’ dataset from food.com, which contains information about various recipes along with user ratings and reviews. The dataset used is relevant for people interested in cooking, nutrition, and recipe recommendations. The data comes in two parts:
 1. **Recipes Dataset**: Contains details about recipes, including preparation time, number of ingredients, steps, and nutritional information.
 2. **Interactions Dataset**: Includes user reviews and ratings, providing insights into recipe performance.


### Question/Why It Matters
The project is centered around the question: **“What types of recipes tend to be healthier, or in other words what types of recipes tend to have a lower calorie count?”** This is an important question to evaluate because with increasing awareness about health and nutrition, many people are seeking healthier recipe options to support their lifestyle. Understanding what components relate to a recipe being lower in calories can help individuals make better dietary choices. This analysis aims to identify key recipe factors, such as preparation time, number of ingredients, and nutritional components, that affect the total calorie count of a recipe. 

### Dataset Information 
The number of rows in the dataset is 231637, the number of columns before cleaning is 12 and after cleaning was 15. The relevant column names and descriptions to our analysis are as follows: 

#### **Recipes Dataset**:
- **`name`**: Recipe name.
- **`nutrition`**: List of nutritional values: 
  - Calories (#): Number of calories
  - Total fat (PDV): Total fat content in PDV
  - Sugar (PDV): Sugar content in PDV
  - Sodium (PDV): Sodium content in PDV
  - Protein (PDV): Protein content in PDV
  - Saturated fat (PDV): Saturated fat content in PDV
  - Carbohydrates (PDV): Carbohydrate content in PDV
- **`n_ingredients`**: Number of ingredients required for the recipe.

---

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning 

1. The recipes data set was merged with the interaction data set with the 'id' of the recipe. This added the rating columns into the recipe data set.

2. In the merged dataset, the ratings of ‘0’ were filled with NaN, since the rating scale was from 1 to 5, which does not include the value of 0. The recipes with ratings of ‘0’ had missing rating data.
   
3. The average rating per recipe was calculated and added as a new column to the dataframe (as a Series).
 
4. Nutritional information was extracted from the ‘nutrition’ column into separate columns for calories, fat, sugar, sodium, protein, etc.
   
5. The missing values were handled by not imputing them since there was no accurate and reliable way to estimate them.

6. Columns unnecessary to our analysis were dropped such as the tag column, ingredient column, minutes column, and more. 


```py
print(recipes.head().to_markdown(index=False))
```

| name                                       |   n_ingredients |   average_rating |   calories (#) |   total_fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated_fat (PDV) |   carbohydrates (PDV) |
|:-------------------------------------------|----------------:|-----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
| arriba   baked winter squash mexican style |               7 |          5       |           51.5 |                 0 |            13 |              0 |               2 |                     0 |                     4 |
| a bit different  breakfast pizza           |               6 |          4.66667 |          173.4 |                18 |             0 |             17 |              22 |                    35 |                     1 |
| all in the kitchen  chili                  |              13 |          4       |          269.8 |                22 |            32 |             48 |              39 |                    27 |                     5 |
| alouette  potatoes                         |              11 |          4.5     |          368.1 |                17 |            10 |              2 |              14 |                     8 |                    20 |
| amish  tomato ketchup  for canning         |               8 |          5       |          352.9 |                 1 |           337 |             23 |               3 |                     0 |                    28 |


### Univariate Analysis

**Distribution of Calories**

 <iframe
 src="assests/calorie-dist.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

This histogram, which shows the distribution of the number of calories across all recipes that are 3000 calories or lower, in order to eliminate extreme outliers, stipulates that the majority of the recipes fall in the 0 to 500 calories range, with a peak at around 150 to 190 calories. This right skewed distribution indicates that while most recipes are moderately low in calories, there still exists a long tail of higher calorie recipes, which helps us understand what is considered a relatively “low-calorie” recipe in terms of this dataset.


**Distribution of Protein**

 <iframe
 src="assests/protein-dist.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

This histogram, which shows the distribution of the protein amount by PDV across all recipes that are 150% PDV or lower, in order to eliminate extreme outliers, stipulates that the main peak of the recipes fall in the 0% to 7% PDV range (~60,000 recipes), and the majority of the recipes (95% of them) fall in the 5% to 50% PDV range. This right skewed distribution indicates that most recipes are relatively low to moderate in protein, but there still exists a long tail of higher protein recipes.


### Bivariate Analysis

**Distribution of Calories by the Number of Ingredients**

 <iframe
 src="assests/calories-dist-by-num-ingredients.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

This box plot, which shows the distribution of the number of ingredients across all recipes that are 20 ingredients or lower by the number of calories across all recipes that are 3000 calories or lower, in order to eliminate extreme outliers, shows a trend: recipes with higher ingredient counts generally have slightly higher calorie content.

**Distribution of Saturated Fat by Calories**

<iframe
 src="assests/satfat-dist-by-calories-scatter.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The scatter plot illustrates the distribution of saturated fat (PDV) by calories, using a filtered recipe dataset that only contains recipes that are 3000 calories or lower, in order to eliminate extreme outliers. The plot suffers from overplotting, since there are so many points on top of one another making it hard to see the general trend.

<iframe
 src="assests/satfat-dist-by-calories.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The box plot is used to address the overplotting issue observed in the scatter plot and displays the distribution of saturated fat (PDV) across different calorie ranges, filtered so that only recipes that are 3000 calories or lower, in order to eliminate extreme outliers, are considered. The graph shows a trend: recipes with higher calorie counts have higher saturated fat values.

### Interesting Aggregates

```py
print(pivot_table.to_markdown(index=False))
```

| ingredient_range   |   calories (#) |   carbohydrates (PDV) |   protein (PDV) |   sodium (PDV) |   sugar (PDV) |   total_fat (PDV) |
|:-------------------|---------------:|----------------------:|----------------:|---------------:|--------------:|------------------:|
| 0-9                |        424.793 |               14.2776 |         28.7566 |        27.4052 |       84.6468 |           32.1586 |
| 10-19              |        539.225 |               17.2994 |         42.5371 |        33.448  |       83.6886 |           41.2413 |
| 20-29              |        720.483 |               20.7042 |         65.8122 |        55.4133 |       86.0834 |           57.2432 |
| 30-39              |       1342.26  |               36.3148 |         99.7037 |       147.667  |      162.593  |          122.648  |

This pivot table displays nutritional information for different ranges of ingredient counts. The data is filtered to include only recipes with 40 or fewer ingredients and is grouped into intervals of 10 ingredients. From the pivot table, we observe that recipes with more ingredients generally have higher average calorie counts and nutritional values. This allows us to identify which recipes are typically healthier, based on their lower calorie content and higher nutritional value.

### Imputation

Missing rating values were not imputed because the ratings of ‘0’ were invalid due to the rating scale being 1-5, there was no reliable way to estimate missing ratings, and the missing ratings were likely missing at random. So these recipes didn’t skew the analysis, ratings of ‘0’ were imputed with NaN.

---

## Framing a Prediction Problem

The goal of this analysis is to **predict calorie count of recipes** based on various features from the dataset. 

### Problem Type
This is a regression problem since calorie count is a continuous numerical variable, the differences between calorie values can be quantitatively measured, and the goal is to predict precise numerical outcomes. 

### Response Variable/Features
The **response variable** is calories, which was extracted from the ‘nutrition’ column. This was chosen as the response variable because the number of calories in a recipe can be used to answer the initial question about which recipes tend to be healthier. 

**Features**
  - `protein`: Protein content (PDV)
  - `sugar`: Sugar content (PDV)
  - `carbohydrates`: Carbohydrate content (PDV)
  - `n_ingredients`: Number of ingredients required for the recipe.
  - `total_fat`: Total fat content (PDV)

**Relevance**: The selected features directly relate to key nutritional factors influencing calorie content.

**Availability**: These features are always available at the time of prediction, as they are from a recipe’s nutritional information. The information known at the “time of prediction” include number of ingredients, preparation time, and nutritional components that may correlate with calories.


### Evaluation Metrics
The evaluation metric is **Mean Squared Error (MSE)**. This was chosen because it penalizes large errors more heavily, it’s commonly used for regression problems, and the square units match people’s intuitive understanding of calorie differences. We will also use **R² Score** as it explains the proportion of variance in calorie count that can be predicted by the selected feature.

Other possible metrics for regression, such as Mean Absolute Error (MAE) or Root Mean Squared Error (RMSE), were considered but ultimately not used as primary metrics. MAE treats all errors equally and doesn’t emphasize larger deviations, which makes it less sensitive to outliers. RMSE, while interpretable in the same units as the target variable (calories), carries the same penalty characteristics as MSE and would lead to similar conclusions, so we chose to report the simpler MSE for consistency and ease of comparison.

---

## Baseline Model

### Model Description 
The baseline model is a Linear Regression model that predicts the calorie content of a recipe based on two quantitative features that are  related to calories: protein content (PDV) and number of ingredients. 

### Features
1. **Quantitative Features**:
   - `protein (PDV)`: Protein content in Percent Daily Value (PDV%).
   - `number of ingredients`: The number of ingredients in the recipe.
   - Protein is a quantiatvie continuous feature, while number of ingredients is a quantitative discrete feature. 
   - Both features are numerical, therefore they require no special encoding but required standardization. Both feature were standardized
     using `StandardScaler` to make the values comparable, as linear regression models are sensitive to the magnitude of the features.

2. **Response Variable**:
   - `calories`: Number of calories, the response variable, measured as a continuous quantitative value.
  
### Model Performance

1. **Mean Squared Error (MSE)**:
   - Train MSE: **93680.658**
   - Test MSE: **93217.755**

   **Interpretation**: The model's predictions differ significantly from the actual calorie values, suggesting that this basic model has difficulty accounting for the variability in calorie content.

2. **R² Score (Coefficient of Determination)**:
   - Train R²: **0.3656**
   - Test R²: **0.3749**
  
   **Interpretation**: The model explains only ~37% of the variance in calorie values.

### Is This a Good Baseline Model?

This is a **weak baseline model**, as it has a low explantory power (low R² score) and prediction accuracy (high MSE). The low R² score suggests that the features chosen (`protein` and `number of ingredients`) are insufficient to predict calories effectively on their own and the high MSE suggests that only utilizing `protein` and `number of ingredients` leads to high error, meaning it does not predict calories well.

---

## Final Model
### Model Description 
The final model uses additional engineered features in order to better predict the calorie content of a recipe based on multiple nutritional information and number of ingredients. It utilizes a more advanced regression model and hypterunes paramteres to increase its predicitve performance.  

### Features
1. **Quantitative Features**:
   - `number of ingredients`: the number of ingredients in the recipe.
   - `total_fat (PDV)`: Total fat content in Percent Daily Value (PDV%).

2. **Engineered Features**:
    - `protein_to_fat_ratio`: This feature captures the ratio of protein to fat content in a recipe. This is a good engineered feature since fat contains more calories per gram (9 cal/g) compared to protein (4 cal/g). Therefore, a higher protein-to-fat ratio often correlates with a lower overall calorie density,  helping to predict calorie content more accurately.
   
    - `carbs_to_fat_ratio`: This feature captures the ratio of carbohydrates to fat content in a recipe. This is a good engineered feature since fat contains more calories per gram (9 cal/g) compared to carbohydrates (4 cal/g). Therefore, a higher carbohydrates-to-fat ratio often correlates with a lower overall calorie density, helping to predict calorie content more accurately.
  
    - `log_sugar` The log transformation addresses skewness in sugar distribution, making relationships between sugar and calorie content more linear and manageable for regression.
  
    These features likely improve model performance as they help to capture more complex relationships between macronutrient compositions and the target variable.

3. **Response Variable**:
   - `calories`: Number of calories, the response variable, measured as a continuous quantitative value.
  
### Preprocessing 
- FunctionTransformer: Custom function compute_ratios_log is used to compute additional features: Protein to Fat Ratio, Carbs to Fat Ratio, Log Sugar
  
- PolynomialFeatures: Applied with degree=2 and interaction_only=True to generate interaction terms among input features. This captures the combined effects of features, enabling the model to learn more complex patterns.

- StandardScaler: Standardizes features by removing the mean and scaling to unit variance. Essential for ensuring that features contribute equally in the Lasso regression model.

### Modeling Algorithim
- Lasso Regression: used to simplify models by L1 regularization, effectively performing feature selection and managing multicollinearity.
   - Lasso can perform feature selection by driving some coefficients to zero, which simplifies the model.
   - It helps with datasets where features are highly correlated, reducing variance in model prediction and overfitting. 

### Best Hyperparameters
Through GridSearchCV, the optimal hyperparameter configuration was found to be:
- `lambda/alpha`: 0.1

The final model uses the engineered features and Lasso with cross-validation to identify optimal hyperparameters. To tune our Lasso regression model, we used GridSearchCV with 5-fold cross-validation to find the optimal value of alpha, the regularization strength. The search spanned alpha values from 0.1 to 100, and the best-performing value was 0.1, which offered a strong balance between model complexity and overfitting control. This approach ensured the model generalized well to unseen data by minimizing the average MSE across validation folds.

  
### Model Performance

1. **Mean Squared Error (MSE)**:
   - Train MSE: **1560.999**
   - Test MSE: **1323.506**
     
   **Interpretation**: The train and test MSE values indicate the average squared difference between the predicted and actual calorie values. The relatively low MSE on both the training and test sets indicate that the model's predictions are more accurate than the baseline and that it generalizes well to unseen data.

2. **R² Score (Coefficient of Determination)**:
   - Train R²: **0.9894**
   - Test R²: **0.9911**
  
   **Interpretation**: The model explains only ~99% of the variance in calorie values. This high degree of variance explanation suggests that the model captures the underlying relationships between the input features and calorie content effectively.

### Final Model Improvement from Baseline

The final model uses the engineered features and Lasso with cross-validation to identify optimal hyperparameters.
The baseline model was a simple linear regression model without feature engineering and parameter tuning. The improvements in the model are  due to the increased complexity of the final model and the addition of features. By comparing mean squared errors (MSE) and R² scores between the training and test sets for both models, the final model shows a decrease in MSE and an increase in R², indicating better fit and generalization to unseen data.

**Visualization of Model Performance**

 <iframe
 src="assests/accuracy-visualization.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

---
Final Project for UMich EECS 398 WN 25 using Recipes and Ratings Dataset 
