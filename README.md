# What Makes a Delicious Recipe Highly Rated?

Randall Bassig

## Introduction

This project will analyze different recipes and ratings from the website Food.com. The dataset contains a variety of different information about individual recipes such as prep time, amount of steps, ingerdients, nutritional information, and unique ratings submitted by diffrent users.

This leads me to the question:

> What characteristics such as ingredients, preparation time, and nutrition can cause users to associate these recipes with a higher on average rating than usual? 

I am specifically analyzing this question because, as a college student, I have been cooked for my entire life through my life by my parents and now bear the responsibility to cook for myself. This project should help me associate certain characteristics to higher rating food to improve my culinary skills. 

In step 2, I went ahead and made a quick analysis of the dataset and found it contains  **83,782 recipes**. The columns relevant are:

- `minutes`: # of minutes to make a recipe
- `n_steps`: # of steps made for a recipe
- `n_ingredients`: # of ingeredients in a recipe
- `nutrition`: nutritional information: calories, fat, sugar, sodium, protein, saturated fat, carbohydrates.
- `tags`: characteristics associated with the recipe.
- `average_rating`: average rating for a recipe.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

To prepare the dataset for analysis, I cleaned and transformed several columns. I first calculated the average rating for each recipe using the user interaction data and merged those values into the recipes dataset. I then parsed the `nutrition` column, which was originally stored as a string representation of a list, into separate numerical columns for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.

I also examined preparation time and other numerical variables for extreme values before performing exploratory analysis. For preparation time visualizations, I focused on recipes that took more than 0 minutes and no more than 250 minutes so that extreme outliers would not dominate the plots.

<iframe
  src="assets/preparation-time-distribution.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

The preparation-time distribution is right-skewed, with most recipes taking substantially less time than the extreme recipes in the dataset. Most recipes are concentrated in the lower preparation-time range.

### Distribution of Ingredients

<iframe
  src="assets/ingredients-distribution.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

The number of ingredients is concentrated around roughly 5 to 12 ingredients, with the highest frequency around 8 to 10 ingredients. The distribution is right-skewed, with relatively few recipes containing more than about 20 ingredients.

### Number of Ingredients and Average Rating

<iframe
  src="assets/ingredients-vs-rating.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

Average ratings remain relatively similar across most ingredient counts, although there are some differences between groups. Recipes with very high ingredient counts were excluded from this visualization because those groups contained relatively few recipes and produced unstable average ratings.

### Average Rating by Calorie Range

| Calorie Range | Average Rating | Number of Recipes |
| --- | ---: | ---: |
| 0-200 | 4.6340 | 24,868 |
| 201-400 | 4.6214 | 27,305 |
| 401-600 | 4.6212 | 14,771 |
| 601-800 | 4.6214 | 6,556 |
| 801-1100 | 4.6218 | 3,820 |

I grouped recipes into calorie ranges and calculated the average rating and number of recipes within each group. The average ratings are very similar across the calorie ranges, with all groups having an average rating around 4.62 to 4.63. The lowest-calorie group has a slightly higher average rating, but the difference is small.

## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
