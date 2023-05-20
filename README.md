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

## Univariate Analysis
<iframe src="assets/fig1.html" width=800 height=600 frameBorder=0></iframe>
