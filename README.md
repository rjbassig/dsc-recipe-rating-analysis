# What Makes a Delicious Recipe Highly Rated?

By Randall Bassig

## Introduction

This project will analyze different recipes and ratings from the website Food.com. The dataset contains a variety of different information about individual recipes such as prep time, amount of steps, ingerdients, nutritional information, and unique ratings submitted by diffrent users.

This leads me to the question:

> What characteristics such as ingredients, preparation time, and nutrition can cause users to associate these recipes with a higher on average rating than usual? 

I am specifically analyzing this question because, as a college student, I have been cooked for my entire life through my life by my parents and now bear the responsibility to cook for myself. This project should help me associate certain characteristics to higher rating food to improve my culinary skills. 

In step 2, I went ahead and made a quick analysis of the dataset and found it contains **83,782 recipes**. The columns relevant are:

- `minutes`: # of minutes to make a recipe
- `n_steps`: # of steps made for a recipe
- `n_ingredients`: # of ingeredients in a recipe
- `nutrition`: nutritional information: calories, fat, sugar, sodium, protein, saturated fat, carbohydrates.
- `tags`: characteristics associated with the recipe.
- `average_rating`: average rating for a recipe.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

For this part, I had to clean and transform several columns from my data set. I first calculated the average rating for each recipe from the user interaction data. With this I merged that into the main dataset for recipes. After that I broke down the `nutrition` column which was used as a string into numerical columns for the following: calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.

I also examined preparation time along with other numerical variables for extreme values before doing the EDA. For preparation time visualizations, I focused on recipes that took more than 0 minutes and no more than 250 minutes so that extreme outliers would not dominate the plots.

### Cleaned DataFrame

Here are the first five rows of the cleaned dataset:

| name | minutes | n_steps | n_ingredients | average_rating |
|:---|---:|---:|---:|---:|
| 1 brownies in the world    best ever | 40 | 10 | 9 | 4 |
| 1 in canada chocolate chip cookies | 45 | 12 | 11 | 5 |
| 412 broccoli casserole | 40 | 6 | 9 | 5 |
| millionaire pound cake | 120 | 7 | 7 | 5 |
| 2000 meatloaf | 90 | 17 | 13 | 5 |

<iframe
  src="assets/preparation-time-distribution.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

The preparation-time distribution of this data set is right-skewed which means most recipes take less time. Most recipes are on the lower preparation-time side.

### Distribution of Ingredients

<iframe
  src="assets/ingredients-distribution.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

The number of ingredients is concentrated around roughly 5 to 12 ingredients and the highest frequency around 8 to 10 ingredients. The distribution is right-skewed with the least amount of recipes being above 20. 

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

### Missingness of Average Rating

The `average_rating` variable has missing values in approximately **3.11%** of recipes. I explored if there may be some relationship between the missingness of `average_rating` and other attributes of a recipe.

The missingness of `average_rating` variable could be potentially **MNAR** since whether or not a recipe gets any ratings can depend on some information which is not present in the dataset. Less popular or less visible on the website recipes, or recipes with lower number of views are less likely to get any ratings. The number of recipe views and the number of times this recipe appeared in the users' feed would be helpful in understanding this pattern of missingness.

### Missingness and Preparation Time

A permutation test was conducted to find out whether missingness in `average_rating` is associated with recipe preparation time. In this analysis, recipe preparation times were limited to above 0 and up to 250 minutes to avoid having extreme values affecting the comparison.

**Null Hypothesis:** Missingness of `average_rating` is unrelated to preparation time.

**Alternative Hypothesis:** Missingness of `average_rating` is related to preparation time.

**Test Statistic:** Difference in mean preparation time of recipes with missing average rating versus non-missing average rating.

**Level of Significance:** 0.05

The difference in mean preparation time was around **8.33 minutes**.

<iframe
  src="assets/missingness-preparation-time.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

The permutation test yielded a p-value of **less than 0.001**. Since the value is less than the alpha level of 0.05, the null hypothesis will be rejected, meaning that there is enough evidence to support the claim that missing average rating and cooking time are correlated.

### Missingness and Protein Content

Furthermore, I conducted a permutation test to see if the missingness of average rating depends on the protein in the recipe.

**Null Hypothesis:** The missingness of `average_rating` is independent of protein content.

**Alternative Hypothesis:** The missingness of `average_rating` depends on protein content.

The difference in averages of the protein in the food was approximately **1.287**, and the permutation test I ran resulted in a p-value of **0.185**. Since this is greater than the significance level of 0.05, I ended up having to fail the null hypothesis. So there is not sufficient evidence to conclude that the missingness of `average_rating` depends on the protein content of a recipe.

## Hypothesis Testing

### Protein Content and Average Rating

During my EDA process, I saw that recipes with higher protein content tended to have a lower average rating than recipes with lower protein content that had higher protein content. I used a permutation test to determine whether this observed difference could be explained by random chance or if there was more to this.

**Null Hypothesis:** Recipes with lower protein content and recipes with higher protein content have around the same average rating. Any observed difference between the groups is completely random .

**Alternative Hypothesis:** Recipes that have a lower protein content have a higher average rating than compared to the recipes with higher protein content.

**Test Statistic:** Using the average rating of lower-protein recipes subtracted by the average rating of higher-protein recipes.

**Significance Level:** 0.05

The reason for choosing the difference in means as my test statistic was that `average_rating` is a numerical variable and I decided to compare average ratings of two groups. My significance level that I used was 0.05 as the criterion to determine if there is enough evidence against the null hypothesis.I divided the recipes into lower- and higher-protein groups using a protein value of 18 as the cutoff. Recipes with protein values less than or equal to 18 were placed in the lower-protein group, while recipes with values greater than 18 were placed in the higher-protein group.

The mean rating for the high protein group was roughly **4.6125**, whereas the mean rating for the low protein group was roughly **4.6379**. This gave us an observed difference of roughly **0.0254**.

I performed **10,000 permutations** by randomly shuffling the protein-group labels and recalculating the difference in average ratings. None of the 10,000 simulated differences were as large as the observed difference, resulting in an estimated p-value of **less than 0.0001**.

Since the p-value is below the significance level of 0.05, I reject the null hypothesis. The data provides strong evidence that recipes with lower protein content tend to have a higher average rating than recipes with higher protein content. However, this result demonstrates an association and does not establish that lower protein content causes higher ratings.

## Framing a Prediction Problem

A **regression model** will be developed to predict the value of `average_rating`. The response variable was selected based on the relationship of the original question to find recipe features which are related to higher average ratings.

For the assessment of the performance of my model, I will use the measure of **Root Mean Squared Error (RMSE)**. It gives a measure of the magnitude of the errors and the error values receive more weight when their magnitude is larger. A lower RMSE value means better predictive performance. Instead of MAE measure, I decided to use RMSE because it puts more emphasis on large prediction errors which is helpful to find such predictions.

For predictions, the features will be limited by the variables that would have been known before the user rated the recipe. It includes features like preparation time, number of steps, number of ingredients, nutrition.

## Baseline Model

My baseline model is a **Linear Regression** model that predicts a recipe's `average_rating` using three features from the original dataset:

- `minutes`: a quantitative feature representing the preparation time of the recipe.
- `n_steps`: a quantitative feature representing the number of steps required to make the recipe.
- `n_ingredients`: a quantitative feature representing the number of ingredients in the recipe.

Since all three features are quantitative, I left them as numerical values using `passthrough` in a `ColumnTransformer`, so no categorical encoding was necessary. The preprocessing and `LinearRegression` model were combined into a single scikit-learn `Pipeline`.

I evaluated the model using RMSE on both the training data and the unseen testing data.

| Dataset | RMSE |
| --- | ---: |
| Training | 0.6419 |
| Testing | 0.6360 |

The training RMSE is **approximately 0.6419**, and the testing RMSE is **approximately 0.6360**. As the difference between them is very small, the model exhibits similar performance on both training and testing data sets and no significant indication of overfitting can be observed.

However, I do not consider the baseline model particularly strong. An RMSE of approximately **0.64** means that the model's predicted ratings can still differ noticeably from the actual ratings. This leaves room to improve the model by engineering additional features and using a model that can capture more complex relationships in the data.

## Final Model

To improve upon my baseline model, I created a final model using a **DecisionTreeRegressor** and engineered two new features:

- `log_minutes`: the logarithm of preparation time, calculated using `log1p(minutes)`. I created this feature because preparation time was heavily right-skewed, so the logarithmic transformation reduces the influence of extremely long preparation times.
- `protein_per_ingredient`: protein content divided by the number of ingredients. I created this feature to represent the amount of protein relative to the complexity and size of a recipe rather than considering protein content by itself.

The final model uses `minutes`, `n_steps`, `n_ingredients`, `protein`, `log_minutes`, and `protein_per_ingredient`. I chose a Decision Tree because it can capture relationships between recipe characteristics and ratings that do not have to be linear. All feature engineering and model training were included within a single scikit-learn `Pipeline`.

Before tuning the model, I chose to tune the `max_depth` hyperparameter. Increasing the maximum depth allows a decision tree to model more complex relationships, but allowing the tree to become too deep can lead to overfitting.

I used **5-fold cross-validation with GridSearchCV** to compare the following values of `max_depth`:

`2, 3, 4, 5, 6, 8, 10, 12`

The best-performing value was **`max_depth = 3`**, with a cross-validation RMSE of approximately **0.6414**.

I then evaluated the selected final model using the same training and testing data used for my baseline model.

| Model | Training RMSE | Testing RMSE |
| --- | ---: | ---: |
| Baseline Linear Regression | 0.6419 | 0.6360 |
| Final Decision Tree | 0.6409 | 0.6354 |

The final model achieved a training RMSE of approximately **0.6409** and a testing RMSE of approximately **0.6354**. This is a slight improvement over the baseline model's testing RMSE of approximately **0.6360**. The similar training and testing RMSE values also suggest that the final model generalizes similarly to unseen data without substantial overfitting.

Although the improvement is small, the final model performs better on the same unseen testing data. The engineered features were chosen based on characteristics of the data rather than simply because they improved the model's score. `log_minutes` addresses the strongly right-skewed preparation-time distribution observed during exploratory analysis, while `protein_per_ingredient` represents nutritional content relative to recipe complexity.

## Fairness Analysis

I evaluated whether my final model performs differently for recipes with shorter versus longer preparation times. I divided the recipes in the test set into two groups using the median preparation time of **35 minutes**:

- **Group X, Shorter Recipes:** preparation time less than or equal to 35 minutes.
- **Group Y, Longer Recipes:** preparation time greater than 35 minutes.

I used **RMSE** as the evaluation metric because my final model is a regression model and RMSE measures the size of its prediction errors.

**Null Hypothesis:** The final model is equally accurate for shorter and longer preparation-time recipes. Any observed difference in RMSE between the two groups is due to random chance.

**Alternative Hypothesis:** The final model's prediction accuracy differs between shorter and longer preparation-time recipes.

**Test Statistic:** RMSE for longer-preparation recipes minus RMSE for shorter-preparation recipes.

**Significance Level:** 0.05

I used the same fitted final model from the previous section without modifying or retraining it. The model produced an RMSE of approximately **0.6107** for shorter recipes and **0.6603** for longer recipes.

| Group | RMSE |
| --- | ---: |
| Shorter Recipes | 0.6107 |
| Longer Recipes | 0.6603 |

The observed difference in RMSE was approximately **0.0496**, with the model having a higher RMSE for longer recipes.

I performed a permutation test by randomly shuffling the preparation-time group labels and recalculating the difference in RMSE. The permutation test produced a p-value of **0.005**.

<iframe
  src="assets/fairness-rmse-permutation.html"
  width="100%"
  height="600"
  frameborder="0">
</iframe>

Since the p-value is 0.005 which is lower than the level of significance 0.05, I reject the null hypothesis. The findings indicate that there is a difference in the prediction accuracy of the final model between recipes with short preparation time and those with long preparation time. From this dataset, the prediction accuracy was lower for the longer recipes.
