# 🍽️ Recipe Nutrition and Rating Analysis
*Author: Lucero Toral*

---


## Introduction



## Data Cleaning and Exploratory Data Analysis

### Data Cleaning


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

<iframe
  src="assets/dist_ratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

<iframe
  src="assets/health_ratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

| is_healthy   |   count |    mean |     std |   min |   25% |   50% |   75% |   max |
|:-------------|--------:|--------:|--------:|------:|------:|------:|------:|------:|
| False        |   70051 | 4.3607  | 1.09391 |     0 |     4 |     5 |     5 |     5 |
| True         |   13730 | 4.32785 | 1.08369 |     0 |     4 |     5 |     5 |     5 |

| rating_high_low   |   calories |   protein |   sugar |
|:------------------|-----------:|----------:|--------:|
| low               |    444.786 |   34.5054 | 71.6494 |
| high              |    423.548 |   32.5444 | 67.3829 |

### Imputation

## Framing a Prediction Problem

### Problem Identification

## Baseline Model

### Baseline Model

## Final Model

### Final Model