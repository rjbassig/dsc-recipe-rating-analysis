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



## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
