# 🍽️ Can Nutrition Predict Recipe Ratings?
*Author: Lucero Toral*

---


## Introduction

In this report, I will be analyzing data of recipes and their respective ratings from food.com. The scraped data contains relevant information about the recipes such as preparation time, relevant tags, nutritional information (total calories, total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV)), recipe steps, and a user-submitted description.

In addition, the scraped data also includes user rating information for each recipe and user-submitted reviews.

The size of each dataset is as follows:
- Recipes: 83,782 rows × 12 columns
- Interactions: 731,927 rows × 5 columns

Having gained an interest in cooking, I am most interested in exploring the nutritional relationship between recipes, ingredients, and user ratings.

In this analysis, I will attempt to answer the question, “Can we predict how favorable a recipe is by its nutritional information?” This is done by predicting user ratings using the nutritional and tag features of the datasets.



## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

The datasets are cleaned by merging them by recipe ID and by calculating the average rating for each recipe.

| **Name**                | **ID**    | **Time (min)** | **Contrib ID** | **Tags**        | **Nutrition**   | **# Steps** | **Steps (First 100 chars)**             | **Description (First 100 chars)**       | **Ingredients (First 100 chars)**       | **# Ingred** | **User ID**    | **Recipe ID**  | **Date**    | **Rating** | **Review (First 100 chars)**            |
|:------------------------|:---------:|:--------------:|:--------------:|:----------------:|:---------------:|:-----------:|:--------------------------------------:|:-------------------------------------:|:--------------------------------------:|:------------:|:--------------:|:--------------:|:-----------:|:----------:|:--------------------------------------:|
| **1 Brownies**           | 333281    | 40             | 985201         | Desserts, Snacks| [138, 10, 50...]| 10          | Heat oven to 350F, line baking dish...  | The most chocolatey, moist, fudgy...  | Chocolate, Butter, Eggs, Sugar...     | 9            | 386585         | 333281         | 2008-11-19  |  4        | These were pretty good, but took f...  |
| **Canada Cookies**       | 453467    | 45             | 1848091        | Cookies, Canada | [595, 46, 211...]| 12          | Preheat oven, sift flours, blend...    | Best school cafeteria cookies...      | Sugar, Butter, Eggs, Vanilla...       | 11           | 424680         | 453467         | 2012-01-26  |  5        | Originally I was gonna cut the re...  |
| **Broccoli Casserole**   | 306168    | 40             | 50969          | Casserole, Side | [194, 20, 6...] | 6           | Preheat oven to 350, mix all ingr...  | Broccoli casserole inspired by...    | Broccoli, Cheese, Onions, Milk...     | 9            | 29782          | 306168         | 2008-12-31  |  5        | This was one of the best broccoli...  |
| **Pound Cake**           | 286009    | 120            | 461724         | Cakes, Dessert  | [878, 63, 326...]| 7           | Grease pan, cream butter, add flo...  | Super rich Southern pound cake...    | Butter, Sugar, Eggs, Flour...        | 7            | 678234         | 286009         | 2009-05-13  |  5        | Why a millionaire pound cake? Be...  |
| **Meatloaf**             | 475785    | 90             | 2202916        | Dinner, Meat    | [267, 30, 12...]| 17          | Pan fry bacon, mince onion, mix ...  | Mediterranean-inspired meatloaf...   | Meat, Bacon, Cheese, Onions...       | 13           | 998231         | 475785         | 2012-03-06  |  5        | Ready, set, cook! Special edition...  |




### Univariate Analysis



<iframe
  src="assets/hist_num_ingred.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

In the first figure, we see the distribution of the number of ingredients in the recipes. This represents the complexity of each recipe, which may influence its perceived flavor profile, as well as the overall nutritional values of each recipe.

<iframe
  src="assets/dist_ratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The second figure shows the distribution of average user rating for the recipes. Note that distribution is skewed far to the higher rating, while having a notable amount of zero ratings. This distibution may suggest that the lowest rated recipes may have distinct features within the data.

### Bivariate Analysis

<iframe
  src="assets/health_ratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

For the third figure, I identify recipes that contain the tag of "healthy" and plot their average rating distributions using violin plots. As we can see, the proportion of 5-star reviews within the data without a "healthy" tag is slightly higher than the distribtion with the tag. This may suggest a high proportion of sweets, desserts, fried, or other recognonized unhealthy foods contributing to high ratings.

### Interesting Aggregates

| is_healthy   |   count |    mean |     std |   min |   25% |   50% |   75% |   max |
|:-------------|--------:|--------:|--------:|------:|------:|------:|------:|------:|
| False        |   70051 | 4.3607  | 1.09391 |     0 |     4 |     5 |     5 |     5 |
| True         |   13730 | 4.32785 | 1.08369 |     0 |     4 |     5 |     5 |     5 |

In the table above, I grouped the rating statistics by whether the recipe is tagged "healthy". The tagged "healthy" recipes have a slighty lower mean rating with a smaller standard deviation to the recipes without the tag. 

| rating_high_low   |   calories |   protein |   sugar |
|:------------------|-----------:|----------:|--------:|
| low               |    444.786 |   34.5054 | 71.6494 |
| high              |    423.548 |   32.5444 | 67.3829 |

Here, I grouped the data by "high" and "low" average ratings and show the average nutritional values of calories, protein, and sugar. The "high" ratings correspond to values of >=4, while the "low" ratings correpond to <4. The lower rated recipes demonstrate slightly higher average calories and sugar level than the highly rated recipes

### Imputation


| **Feature**         | **Missing Values** |
|---------------------|-------------------|
| **`name`**           | 1                 |
| **`id`**             | 0                 |
| **`minutes`**        | 0                 |
| **`contributor_id`** | 0                 |
| **`submitted`**      | 0                 |
| **`tags`**           | 0                 |
| **`nutrition`**      | 0                 |
| **`n_steps`**        | 0                 |
| **`steps`**          | 0                 |
| **`description`**    | 114               |
| **`ingredients`**    | 0                 |
| **`n_ingredients`**  | 0                 |
| **`user_id`**        | 1                 |
| **`recipe_id`**      | 1                 |
| **`date`**           | 1                 |
| **`rating`**         | 1                 |
| **`review`**         | 58                |

This table shows the number of missing values for each column in our combined dataset. 
We are primarily interest in minutes, tags, nutrition, and rating features.

Since there is only one missing data point in the ratings column, imputation isn't necessary. However, for simplicity we will mean impute the single missing data.

## Framing a Prediction Problem

We will train a model to predict recipe rating using the information of nutrition, preparation time, submitted tags, and # of steps from the datasets. 

This a regression problem due to the recipes' average ratings being continous between 0 and 5. (i.e. scores containing off integer values 4.33, 2.57, etc...)

The evaluation metric used is MAE (Mean Absolute Error), this was chosen over other metrics due to its robustness to outliers and easy interpretation.

## Baseline Model


For a baseline model, we train a Linear Regression model that takes in quantitative and nominal features to predict the average user rating.

The selected quantitative features are:

| **Feature**        | **Description**                                   |
|--------------------|---------------------------------------------------|
| **`minutes`**      | Time (in minutes) to prepare the recipe.          |
| **`calories`**     | Total calories in the recipe.                    |
| **`total_fat`**    | Total fat content in the recipe.                 |
| **`sugar`**        | Total sugar content in the recipe.               |
| **`sodium`**       | Total sodium content in the recipe.              |
| **`protein`**      | Total protein content in the recipe.             |
| **`saturated_fat`**| Total saturated fat content.                    |
| **`carbohydrates`**| Total carbohydrate content in the recipe.       |

These features represent the preparation complexity and nutrional information of the recipes.

The selected catagorical feature:

|**Feature**        | **Description**                                   |
|-------------------|---------------------------------------------------|
| **`tags_str`**    | List of tags (like "healthy", "lunch", etc.) |

No ordinal features were selected.

The quantitative features were preprocessed with scikit's StandardScaler, while the catagorical features are encoded with OneHotEncoder, to represent the tags as binary features.

The model performed with a MAE score of 0.760, meaning the prediction is on average off by 0.760. Since the potential score range of 0 - 5, the model is not terribly off but considering Figure 2 that majority ratings are between 4 and 5, the model may not be identifying the lower scores.



## Final Model


For the final model, we engineered the following features:

| **Feature Name**             | **How It Was Created**                          | **Why It’s Useful** |
|-----------------------------|------------------------------------------------|---------------------|
| **`log_minutes`**             | `log1p(minutes)` (log-transformed)             | Log transformation reduces skew |
| **`sodium_calorie_ratio`**    | `sodium / (calories + 1e-5)`                    | How much sodium there is relative to total calories, which may influence taste (salty food can have higher or lower ratings). |
| **`total_fat_calorie_ratio`** | `total_fat / (calories + 1e-5)`                 |  Fatty foods like desserts may be rated differently than leaner recipes. |
| **`sugar_calorie_ratio`**     | `sugar / (calories + 1e-5)`                     | Tracks how much of the recipe's calories come from sugar. |
| **`protein_calorie_ratio`**   | `protein / (calories + 1e-5)`                   | Protein may be important to health-conscious users. |
| **`saturated_fat_calorie_ratio`** | `saturated_fat / (calories + 1e-5)`         | Helps identify recipes with a high proportion of "bad fats" |
| **`carbohydrates_calorie_ratio`**| `carbohydrates / (calories + 1e-5)`         | Indicates how "carb-dense" the recipe is. (e.g., high-carb desserts vs. low-carb meals). |

The preparation time feature was log scaled to reduce the influence of significant outliers. 

The nutritional features were all scaled with the recipe's total calories. This was chosen because total calories is correlated to nutritional values for each recipe. Therefore, these nutrition ratios provide a better metric of the healthiness each recipe. It will also help highlight the percieved tastes of the recipes, as "saltier" foods would have a higher sodium ratio, "sweeter" foods have a higher sugar to calorie ratio.

We choose to implement the LASSO regression, due to the many catagorical tag features from the OnehotEncoding. LASSO should learn to disregard unimportant features from irrelevant tags. 

We performed a gridsearch of the alpha hyperparameter, with the possible values of [0.01, 0.1, 1]. In addition, we perform cross-validation with 3-folds to validate the optimal alpha value.

The hyperparameter that performed best was alpha = 0.01, which demonstrated an MAE value of 0.756.

The final model with the additional feature engineering is a small improvement over the base line. (MAE 0.756 vs. MAE 0.760)
Further improvement to the existing model can be done by gridsearching over more hyperparameters and increasing the max iterations from the default 1000 intereations.

Additionally, we have assumed a linear relationship to predict the average ratings. Training a non-linear model may produce better results.

