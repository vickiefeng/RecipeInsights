# Recipe Insights
by Vickie Feng

This is a project for DSC 80 at UCSD that analyzes the relationship between recipe preparation time and the corresponding average rating.

## Introduction
This dataset is a collection of data scrapped from Food.com, combining information on recipes with user ratings and reviews. From this dataset, we can gain insights into the relationship between recipe attributes and the corresponding user-given ratings. From analyzing this dataset, we can gain a better understanding of the length of recipes that tend to receive favorable reviews and answer the question: **How does the cooking time (in minutes) of a recipe relate to its average rating?**

There were a total of 229568 rows and 10 relevant columns in the merged dataframe I created: 

| Column | Description |
| --- | --- |
| `name` | Name of recipe |
| `id` | Recipe ID |
| `minutes` | Minutes to prepare recipe |
| `n_steps` | Number of steps in recipe |
| `description` | User-provided description |
| `ingredients` | Ingredients in recipe |
| `n_ingredients` | Number of ingredients in recipe |
| `rating` | Rating given by user |
| `avg_rating`| Average rating of recipe | 
| `calories` | Number of calories in recipe |

## Cleaning and EDA

### Data Cleaning
**Merging**: To create the merged dataframe, I did a left merge on the recipes and interactions datasets based on the `id` and `recipe_id` columns of the `recipes` and `interactions` datasets, respectively. I dropped any columns that were either duplicates or irrelevant to my data exploration. I also dropped the row with index 144443 because it did not contain any information from the interaction dataset. 
  
**NaN values**: I located all the rows where the merged dataframe’s rating column were 0 and filled those zero values with NaN values. Because the rating system is from one to five, a rating of 0 indicates that a rating was not given. As follows, these missing ratings will not skew any calculations and analyses involving ratings. 

**Creating additional columns**: I split the ‘nutrition’ column into seven separate columns to allow for easier access to the specific nutritional components of the recipes. 

**Discarding outliers**: I discarded any rows where the number of minutes exceeded the 98th percentile of minutes because that data consisted of extreme outliers, including recipes that took up to a month to finish. 

The first five rows of the cleaned dataframe is shown below:

|    | name                                 |     id |   minutes |   n_steps | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                    |   n_ingredients |   rating |   avg_rating |   calories |
|---:|:-------------------------------------|-------:|----------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|-------------:|-----------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |        10 | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |        4 |            4 |      138.4 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |        12 | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |        5 |            5 |      595.1 |
|  2 | 412 broccoli casserole               | 306168 |        40 |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |            5 |      194.8 |
|  3 | 412 broccoli casserole               | 306168 |        40 |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |            5 |      194.8 |
|  4 | 412 broccoli casserole               | 306168 |        40 |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |            5 |      194.8 |

### Univariate Analysis
The following histogram shows the probability distribution of the average ratings. We can make note of the fact that the average rating is very high, where nearly 80% of ratings fall in the 4.5 - 5 range. 

<iframe src="assets/fig2.html" width=800 height=600 frameBorder=0></iframe>

Below is a histogram that displays the distribution of recipe minutes. We can see that it is highly skewed to the left, and the vast majority of recipes are completed in or less than 120 minutes. 

<iframe src="assets/fig1.html" width=800 height=600 frameBorder=0></iframe>

We can further explore how the number of minutes correlates with the average ratings with our bivariate analysis.

### Bivariate Analysis
The following scatterplot examines the relationship between the number of minutes a recipe takes and its average rating, the following scatterplot. Although the plot doesn't show a clear linear relationship, we can see that there is a dense concentration of data points in the upper left corner of the plot, signifying that a high number of recipes with short to relatively moderate preparation times (less than 100 minutes) were rated highly. This would indicate that **the shorter the recipe time is, the higher the average rating**.

<iframe src="assets/fig3.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates
By grouping the data by rating then aggregating by the mean on various columns, it is clear that certain attributes of a recipe have more variance across ratings. For example, the pivot table below shows that as ratings increase, the average number of minutes tends to decrease. This is also the case for calorie count. On the other hand, the number of ingredients is roughly the same across ratings.

|   rating |   minutes |   calories |   n_ingredients |
|---------:|----------:|-----------:|----------------:|
|        1 |   64.9795 |    479.959 |         8.88805 |
|        2 |   63.3552 |    446.694 |         9.20973 |
|        3 |   59.176  |    422.896 |         9.17818 |
|        4 |   53.9407 |    404.05  |         9.07601 |
|        5 |   52.106  |    412.834 |         9.03409 |

## Assessment of Missingness

### NMAR Analysis	
Three columns in the cleaned dataset contain missing values: `description`, `rating`, and `avg_rating`. I believe that the column `rating` is NMAR (Not Missing At Random). The missingness of this rating could stem from user behavior, such as a user choosing to only rate recipes that they particularly like/dislike. This would mean that the chance that a value in `rating` is missing is dependent on the value itself.

### Missingness Dependency
To test the missingness of the `avg_rating` column on the `n_steps` column, I performed permutation testing. First, I created a separate  column, `rating_missing`, to assign True and False values to whether a row was missing an average rating. 

For this test, the null hypothesis is: **The distribution of the number of steps when the average rating is given is the same as when the average rating is missing. The difference between the two observed samples is due to chance.** 

Conversely, the alternative hypothesis is: **The distributions of the number of steps of the two groups are different and not due to chance.**

The following histogram shows the distribution of the number of steps by missingness of the average rating. For these distributions, we can use the K-S statistic as a test statistic to examine the difference between the distributions.  

<iframe src="assets/rating_missingness.html" width=800 height=600 frameBorder=0></iframe>

Using a significance level of 5%, we can calculate the observed test statistic and perform the permutation test 1000 times by shuffling the `rating_missing` column at random to obtain each test statistic. From there, we can calculate the p-value. In doing so, we obtain a p-value of 0.0 and the following distribution: 

<iframe src="assets/fig4.html" width=800 height=600 frameBorder=0></iframe>

Both the p-value and the histogram results indicate that we can reject the null hypothesis at the 0.05 significance level. Thus, we can conclude that the `avg_rating` column does depend on the `n_steps` column. An everyday person may find that the more steps, the more tedious the cooking process, and thus, rate the recipe lower based on the cooking experience. 

We can also test the missingness of the `description` column on presence of olive oil in a recipe. To do this, I created two separate columns, `has_olive_oil`, which assigns True and False values to whether a recipe contains olive oil in its `ingredients` information and `desc_missing`, which assigns True and False values to whether a recipe's description is missing. From there, we can create a conditional distribution by utilizing a pivot table that lists the proportions of recipes that contain or do not contain olive oil and do or do not have a description. Using this conditional distribution, we can create a grouped bar chart that displays this information visually. 

<iframe src="assets/fig5.html" width=800 height=600 frameBorder=0></iframe>

We can make note of the fact that the two distributions are extremely similar, regardless of whether a recipe contains olive oil. Again, we can perform a permutation test to determine if there is any significant difference between the distributions. 

For this test, the null hypothesis is: **There is no significant difference in the distribution of description for recipes with and without olive oil.** 

Conversely, the alternative hypothesis is: **There is a significant difference in the distribution of description for recipes with and without olive oil.**

The following histogram shows the distribution of the number of steps by missingness of the description. For these categorical distributions, we can use TVD as a test statistic to examine the difference.  

<iframe src="assets/fig6.html" width=800 height=600 frameBorder=0></iframe>

Using a significance level of 5%, we can calculate the observed test statistic and perform the permutation test 1000 times by shuffling the `desc_missing` column at random to obtain each test statistic. We fail to reject the null hypothesis, as the observed TVD is less than the 0.05 significance level. Thus, we can conclude that the `description` column does not depend on if a recipe contains olive oil. 

## Hypothesis Testing
Let's circle back to the central question at hand: **How does the cooking time (in minutes) of a recipe relate to its average rating?** To answer this question and see if there's a relationship between the two, we can perform a permutation test. 

Let the null hypothesis be: **The preparation time of a recipe does not influence the average rating of recipes.**

The alternative hypothesis is: **The shorter the time it takes to prepare of a recipe, the higher the average rating of the recipe.**

The test statistic I chose for this test is the signed difference in means. This is because my distributions are numeric and my alternative hypothesis is directional. I also used a significance level of 0.05. To do this permutation test, I took the signed difference in means of the average ratings of recipes with preparation times less than 60 minutes and the average ratings of recipes with preparation times greater than 60 minutes. 60 minutes as a threshold would separate what could be deemed a relatively short to moderate time to make a recipe, and anything greater a long time. I shuffled the `minutes` column 1000 times and the following histogram displays the results of the permutation test:

<iframe src="assets/fig7.html" width=800 height=600 frameBorder=0></iframe>

As we can see, the p-value is 0.0, which is less than the set significance level of 0.05. As such, we say that we fail to reject the null hypothesis. We can see that there is evidence that suggests that there is a relationship between the preparation time of a recipe and its average rating, with lower recipe times tending toward higher ratings and higher recipe times tending toward lower ratings. However, it is important to note that the conclusions drawn from this analysis are based on statistical inference and cannot definitively prove the relationship.
