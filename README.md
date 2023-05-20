# Recipe Insights
by Vickie Feng

This is a project for DSC 80 at UCSD that analyzes the relationship between recipe preparation time and the corresponding average rating.

## Introduction
This dataset is a collection of data scrapped from Food.com, combining information on recipes with user ratings and reviews. From this dataset, we can gain insights into the relationship between recipe attributes and the corresponding user-given ratings. From analyzing this dataset, we can gain a better understanding of the length of recipes that tend to receive favorable reviews and answer the question: **How does the cooking time (in minutes) of a recipe relate to its average rating?**

To create the merged dataframe, I did a left merge on the recipes and interactions datasets based on the ‘id’ and ‘recipe_id’ columns of the `recipes` and `interactions` datasets, respectively. I dropped the columns ‘recipe_id’, ‘review’, ‘contributor_id’, ‘submitted’, ‘date’, and ‘user_id’, as these columns were either duplicates or irrelevant to my data exploration. I also dropped the row with index 144443 because it did not contain any information from the interaction dataset. There were a total of 234206 rows and 18 relevant columns: 



## Cleaning and EDA


