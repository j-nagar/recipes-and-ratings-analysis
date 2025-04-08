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
MAKE EDITS The number of rows in the dataset before cleaning is BLANK, and the number of rows in the dataset after cleaning is BLANK.

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

<iframe src="assets/10-80-enrollment.html" width=800 height=600 frameBorder=0></iframe>

---

## Framing a Prediction Problem

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

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

---

## Baseline Model


---

## Final Model


---
