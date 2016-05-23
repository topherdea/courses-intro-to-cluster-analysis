---
title       : Introduction to Cluster Analysis
description : This course will teach you the basics of cluster analysis.
attachments :

--- type:NormalExercise lang:r xp:100 skills:1 key:211e1551ba
## Hierarchical Clustering

One of the most basic forms of cluster analysis is the hierarchical cluster. Hierarchical clustering measures disimilarity. Disimilarity can be thought of as distance from one observation to another. 

To execute a hierarchical cluster we will first change our data to matrix form, calculate distance, preform the analysis, and the plot the cluster analysis. 

A dataset with a selection of cars, `mtcars`, is available in the workspace.

*** =instructions
- View the structure of your data.
- Convert the data set to matrix format with `as.matrix()`, assign it to the object `cars`.
- Calculate the distance of the `cars` object with `dist()` and assign it to `dist`.
- Use `hclust()` to preform your cluster of the `dist` data, assign it to `h_clust`.
- Plot `h_clust`

*** =hint
- Use `str()` for the first instruction.
- Did you assign the matrix to `cars`?
- Did you preform `hclust()` on the right data?
- Did you plot `h_clust`?

*** =pre_exercise_code
```{r}
# Pre-load dplyr to access mtcars
library(dplyr)

# load mtcars:
mtcars <- data(mtcars)
```

*** =sample_code
```{r}
# mtcars is available in your workspace

# Check out the structure of mtcars


# Create a new matrix called "cars"


# Calculate the distance

# Perform a hierarchical cluster

#Plot h_clust
```

*** =solution
```{r}
# mtcars is available in your workspace

# Check out the structure of mtcars
str(mtcars)

# Create a new matrix called "cars"
cars <- as.matrix(mtcars)

# Calculate the distance
dist <- dist(cars)

# Perform a hierarchical cluster
h_clust <- hclust(dist)

#Plot h_clust
plot(h_clust)
```

*** =sct
```{r}
# The sct section defines the Submission Correctness Tests (SCTs) used to
# evaluate the student's response. All functions used here are defined in the 
# testwhat R package. Documentation can also be found at github.com/datacamp/testwhat/wiki

# Test whether the function str is called with the correct argument, object
# If it is not called, print something informative
# If it is called, but called incorrectly, print something else
test_function("str", args = "mtcars",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(___)` with the correct argument, `mtcars`.")

test_function("as.matrix", args ="mtcars",
              not_called_msg = "You didn't call `as.matrix`",
              incorrect_msg = "You didn't call `as.matrix(___)` with the correct object.")

test_function("hclust", args = "dist",
              not_called_msg = "You didn't call `hclust`",
              incorrect_msg = "You didn't call `hclust` with the correct object.")

test_function("plot", args = "h_clust")

# Test the objeects 
test_object("dist")
test_object("cars")


test_error()

# Final message the student will see upon completing the exercise
success_msg("Good work!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1839b51b1b
## A really bad movie

Have a look at the plot that showed up in the viewer to the right. Which type of movie has the worst rating assigned to it?

*** =instructions
- Adventure
- Action
- Animation
- Comedy
- TEST

*** =hint
Have a look at the plot. Which color does the point with the lowest rating have?

*** =pre_exercise_code
```{r}
library(dplyr)
mtcars <- data("mtcars")
# The pre exercise code runs code to initialize the user's workspace. You can use it for several things:

# 1. Preload a dataset. The code below will read the csv that is stored at the URL's location.
# The movies variable will be available in the user's console.
movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

# 2. Pre-load packages, so that users don't have to do this manually.
library(ggplot2)

# 3. Create a plot in the viewer, that students can check out while reading the exercise
ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

*** =sct
```{r}
# The sct section defines the Submission Correctness Tests (SCTs) used to
# evaluate the student's response. All functions used here are defined in the 
# testwhat R package

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."

# Use test_mc() to grade multiple choice exercises. 
# Pass the correct option (Action, option 2 in the instructions) to correct.
# Pass the feedback messages, both positive and negative, to feedback_msgs in the appropriate order.
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad)) 
```

