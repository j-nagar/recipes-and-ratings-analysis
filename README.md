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
The number of rows in the dataset is 231637, the number of columns before cleaning is 12 and after cleaning was 15. The relevant column names and decriptions to our analysis are as follows: 

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

To clean the data, first the recipes and interactions datasets were merged using a left merge. Then, the ratings of ‘0’ were replaced with NaN, since the rating scale was from 1 to 5, and the ratings of ‘0’ were likely missing data. Next, nutritional information was extracted from the ‘nutrition’ column into separate columns for calories, fat, sugar, sodium, protein, etc. Then, the average ratings per recipe was calculated and added as a new column to the dataframe. The missing values were handled but not imputing them since there was no accurate and reliable way to estimate them. 

| name                                       |     id |   minutes | nutrition                                  |   n_steps | ingredients                                                                                                                                                                                       |   n_ingredients |   average_rating |   calories (#) |   total_fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated_fat (PDV) |   carbohydrates (PDV) |
|:-------------------------------------------|-------:|----------:|:-------------------------------------------|----------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
| arriba   baked winter squash mexican style | 137739 |        55 | [51.5, 0.0, 13.0, 0.0, 2.0, 0.0, 4.0]      |        11 | ['winter squash', 'mexican seasoning', 'mixed spice', 'honey', 'butter', 'olive oil', 'salt']                                                                                                     |               7 |          5       |           51.5 |                 0 |            13 |              0 |               2 |                     0 |                     4 |
| a bit different  breakfast pizza           |  31490 |        30 | [173.4, 18.0, 0.0, 17.0, 22.0, 35.0, 1.0]  |         9 | ['prepared pizza crust', 'sausage patty', 'eggs', 'milk', 'salt and pepper', 'cheese']                                                                                                            |               6 |          4.66667 |          173.4 |                18 |             0 |             17 |              22 |                    35 |                     1 |
| all in the kitchen  chili                  | 112140 |       130 | [269.8, 22.0, 32.0, 48.0, 39.0, 27.0, 5.0] |         6 | ['ground beef', 'yellow onions', 'diced tomatoes', 'tomato paste', 'tomato soup', 'rotel tomatoes', 'kidney beans', 'water', 'chili powder', 'ground cumin', 'salt', 'lettuce', 'cheddar cheese'] |              13 |          4       |          269.8 |                22 |            32 |             48 |              39 |                    27 |                     5 |
| alouette  potatoes                         |  59389 |        45 | [368.1, 17.0, 10.0, 2.0, 14.0, 8.0, 20.0]  |        11 | ['spreadable cheese with garlic and herbs', 'new potatoes', 'shallots', 'parsley', 'tarragon', 'olive oil', 'red wine vinegar', 'salt', 'pepper', 'red bell pepper', 'yellow bell pepper']        |              11 |          4.5     |          368.1 |                17 |            10 |              2 |              14 |                     8 |                    20 |
| amish  tomato ketchup  for canning         |  44061 |       190 | [352.9, 1.0, 337.0, 23.0, 3.0, 0.0, 28.0]  |         5 | ['tomato juice', 'apple cider vinegar', 'sugar', 'salt', 'pepper', 'clove oil', 'cinnamon oil', 'dry mustard']                                                                                    |               8 |          5       |          352.9 |                 1 |           337 |             23 |               3 |                     0 |                    28 |

### Univariate Analysis

Distribution of Calories

 <iframe
 src="assests/calorie-dist.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

ADD DETAIL This histogram shows the distribution of the number of calories across all recipes. It can be seen that most recipes fall in the 0 to 500 calories, with the histogram having a right skew. This helps us understand what is relatively considered a “low-calorie” recipe in terms of this dataset.


Distribution of Protein

 <iframe
 src="assests/protein-dist.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

### Bivariate Analysis

Distribution of Calories by the Number of Ingredients

 <iframe
 src="assests/calories-dist-by-num-ingredients.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

ADD DETAIL This box plot examines the relationship between calorie count and the number of ingredients. We observe FILL IN. This suggests that ingredient count isn’t an ideal predictor of calorie content in a recipe.


Distribution of Saturated Fat by Calories

 <iframe
 src="assests/satfat-dist-by-calories"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>


Distribution of Carbohydrates Fat by Calories

 <iframe
 src="assests/carbs-dist-by-calories"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

### Interesting Aggregates

```py
print(pivot_table.to_markdown(index=False))
```

| ingredient_range   |   calories (#) |   carbohydrates (PDV) |   protein (PDV) |   sodium (PDV) |   sugar (PDV) |   total_fat (PDV) |
|:-------------------|---------------:|----------------------:|----------------:|---------------:|--------------:|------------------:|
| 0-4                |        424.718 |               14.2706 |         28.754  |        27.4005 |       84.6067 |           32.1605 |
| 10-14              |        537.951 |               17.2434 |         42.515  |        33.4009 |       83.1856 |           41.1414 |
| 20-24              |        706.739 |               19.9892 |         65.6583 |        55.3213 |       79.5605 |           56.355  |
| 30-34              |       1319.31  |               35.6863 |         94.0392 |       105.882  |      150.098  |          122.118  |
| 40-44              |        810.333 |               20      |        113.333  |        40.3333 |      124      |           56.3333 |

This pivot table shows average calorie counts grouped by recipe tags. We can see that recipes tagged as TAG1 tend to have HIGHERorLOWER calories than those tagged as TAG2. This helps identify which types of recipes are generally healthier when targeting weight loss.

### Imputation

Missing rating values were not imputed because the ratings of ‘0’ were invalid due to the rating scale being 1-5, there was no reliable way to estimate missing ratings, and the missing ratings were likely missing at random. So these recipes didn’t skew the analysis, ratings of ‘0’ were imputed with NaN.
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
