# Calorie Counter
by Jamila Nagarwala and Mehek Gupta (jnagar@umich.edu and mehekgup@umich.edu)

Final Project for UMich EECS 398 WN 25 using Recipes and Ratings Dataset 

---

## Introduction

This project analyzes the ‘Recipes and Ratings’ dataset from food.com, which contains information about various recipes along with user ratings and reviews. The dataset used is relevant for people interested in cooking, nutrition, and recipe recommendations. The data comes in two parts:
 1. **Recipes Dataset**: Contains details about recipes, including preparation time, number of ingredients, steps, and nutritional information.
 2. **Interactions Dataset**: Includes user reviews and ratings, providing insights into recipe performance.


### Question/Why It Matters
The project is centered around the question: “What types of recipes tend to be healthier, or in other words what types of recipes tend to have a lower calorie count?” This is an important question to evaluate because with increasing awareness about health and nutrition, many people are seeking healthier recipe options to support their lifestyle. Understanding what components relate to a recipe being lower in calories can help individuals make better dietary choices. This analysis aims to identify key recipe factors, such as preparation time, number of ingredients, and nutritional components, that affect the total calorie count of a recipe. 

### Dataset Information 
MAKE EDITS The number of rows in the dataset before cleaning is BLANK, and the number of rows in the dataset after cleaning is BLANK. The relevant column names and decriptions to our analysis are as follows: 

#### **Recipes Dataset**:
- **`name`**: Recipe name.
- **`nutrition`**: List of nutritional values: 
  - Calories (#)
  - Total fat (PDV)
  - Sugar (PDV)
  - Sodium (PDV)
  - Protein (PDV)
  - Saturated fat (PDV)
  - Carbohydrates (PDV)
- **`n_steps`**: Number of steps in the recipe preparation process.
- **`n_ingredients`**: Number of ingredients required for the recipe.

#### **Interactions Dataset**:
- **`recipe_id`**: Unique identifier for each recipe.
- **`rating`**: User-provided rating for the recipe (from 1 to 5).

---

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

#### hello 

### Univariate Analysis

### Bivariate Analysis

### Interesting Aggregates

### Imputation


```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |


<iframe src="assets/10-80-enrollment.html" width=800 height=600 frameBorder=0></iframe>

---

## Framing a Prediction Problem

The goal of this analysis is to predict calorie count of recipes based on various features from the dataset. 

### Problem Type
This is a regression problem since calorie count is a continuous numerical variable, the differences between calorie values can be quantitatively measured, and the goal is to predict precise numerical outcomes. 

### Response Variable/Features
The **response variable** is calories, which was extracted from the ‘nutrition’ column. This was chosen as the response variable because number of calories in a recipe can be used to answers the initial question about which recipes tend to be healthier. 

**Features**
  - `protein`: Protein content (PDV%).
  - `sugar`: Sugar content (PDV%).
  - `carbohydrates`: Carbohydrate content (PDV%).
    
**Relevance**: The selected features directly relate to key nutritional factors influencing calorie content.

**Availability**: These features are always available at the time of prediction, as they are from a recipe’s nutritional information. The information known at the “time of prediction” include number of ingredients, preparation time, and nutritional components that may correlate with calories.


### Evaluation Metrics
The evaluation metric is **Mean Squared Error (MSE)**. This was chosen because it penalizes large errors more heavily, it’s commonly used for regression problems, and the square units match people’s intuitive understanding of calorie differences. We will also use **R² Score** as it explains the proportion of variance in calorie count that can be predicted by the selected feature.

---

## Baseline Model


---

## Final Model


---
