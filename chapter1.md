---
title       : Introduction to Cluster Analysis
description : This course will teach you the basics of cluster analysis.
attachments :

--- type:NormalExercise lang:r xp:100 skills:1 
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
- Did you calculate the distance? 
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

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 
## Quiz Time: Dissimilarity

How do we measure dissimilarity?

*** =instructions
- Standard Deviations
- RMSE
- Variance
- Distance

*** =hint
Have a look at the solution, what did we calculate from the matrix?

*** =pre_exercise_code
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
# testwhat R package

msg_bad <- "That is not correct!"
msg_success <- "Exactly! We calculate distance and use that as a measure of dissimilarity."

# Use test_mc() to grade multiple choice exercises. 
# Pass the correct option (Action, option 2 in the instructions) to correct.
# Pass the feedback messages, both positive and negative, to feedback_msgs in the appropriate order.
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_success)) 
```

