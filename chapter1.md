---
title       : Introduction to Cluster Analysis
description : This course will teach you the basics of cluster analysis.
attachments :

--- type:NormalExercise lang:r xp:100 skills:1  key:211e1551ba
## Hierarchical Clustering

One of the most basic forms of cluster analysis is the hierarchical cluster. Hierarchical clustering measures disimilarity. Disimilarity can be thought of as distance from one observation to another. 

To execute a hierarchical cluster we will first change our data to matrix form, calculate distance, preform the analysis, and the plot the cluster analysis. 

A dataset with a selection of cars, `mtcars`, is available in the workspace.

*** =instructions
- View the structure of your data.
- Convert the data set to matrix format with `as.matrix()`, assign it to the object `cars`.
- Calculate the distance of the `cars` object with `dist()` and assign it to `distance`.
- Use `hclust()` to preform your cluster of the `distance` data, assign it to `h_clust`.
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

# Plot h_clust

```

*** =solution
```{r}
# mtcars is available in your workspace

# Check out the structure of mtcars
str(mtcars)

# Create a new matrix called "cars"
cars <- as.matrix(mtcars)

# Calculate the distance
distance <- dist(cars)

# Perform a hierarchical cluster
h_clust <- hclust(distance)

# Plot h_clust
plot(h_clust)
```

*** =sct
```{r}
# Test whether the function str is called with the correct argument, object
# If it is not called, print something informative
# If it is called, but called incorrectly, print something else

test_function("plot", args = "x",
              incorrect_msg = "You didn't call `plot(___)` with the correct argument, `h_clust`")

test_function("str", args = "object",
              incorrect_msg = "You didn't call `str(___)` with the correct argument, `mtcars`.")

test_function("as.matrix", args ="x",
              incorrect_msg = "You didn't call `as.matrix(___)` with the correct object.")

test_output_contains("h_clust")


# Test the objects 
test_object("distance")
test_object("cars")


test_error()

# Final message the student will see upon completing the exercise
success_msg("Good work!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1  key:a6e6db2517
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
--- type:NormalExercise lang:r xp:100 skills:1  key:c0b56cff17
## K-Means Cluster

K-Means clustering is one of the most basic, and most used unsupervised algorithims. The main idea is to generate **k** number of clusters, or groups based on a mean center. We want each cluster to be as far from each other as possible. If clustered, we assume that each cluster is different from another. 

Creating these clusters is fairly easy and requires you to indicate how many clusters you are searching for. K-means is performed using the `kmeans()`function. The function requires 2 arguments. The first argument passed is the matrix, and the second is the number (**k**) of clusters.

*** =instructions
- Preform a k-means cluster with 5 clusters and assign it to object `fit`.
- Subset data by cluster with `aggregate()` function.
- Create a new data frame with `cars` and `fit$cluster`, assign it to `cluster_cars`.

*** =hint
- Did you assign the correct number of clusters?
- Did you provide the correct argument for `aggregate()`
- Did you call the `data.frame()` with the correct arguments?

*** =pre_exercise_code
```{r}
set.seed(0)
library(dplyr)
data(mtcars)
cars <- as.matrix(mtcars)
```

*** =sample_code
```{r}
# The cars data is preloaded into your workspace.


# Preform your k-means cluster


# Aggregate your cars data by cluster fits
aggregate(___, by=list(fit$cluster), FUN = mean)

# Create a new data frame with the cars and fit data
```

*** =solution
```{r}
# The cars data is preloaded into your workspace.


# Preform your k-means cluster
fit <- kmeans(cars, 5)

# Aggregate your cars data by cluster fits
aggregate(cars, by=list(fit$cluster), FUN = mean)

# Create a new data frame with the cars and fit data
cluster_cars <- data.frame(cars, fit$cluster)
```

*** =sct
```{r}
#First Instruction
test_object("fit")

#Second Instruction
test_student_typed("aggregate(cars, by=list(fit$cluster), FUN = mean)", 
                  not_typed_msg = "Something is wrong with `aggregate()`. Take another look at the instruction.")
                  
#Third Instruction
test_function("data.frame",
              incorrect_msg = "Did you call cars & fit$cluster?")
test_object("cluster_cars")

test_error()

# Final message the student will see upon completing the exercise
success_msg("Good work!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:36e8b9e8b4
##Understanding your cluster.

Take a look at your console, and try running the code.

This graph was created using ggvis. Check out the course on ggvis!

Which cluster has the best mileage?

*** =instructions
- 1
- 2
- 3
- 4
- 5

*** =hint
Look at the legend and the color of the dots!

*** =pre_exercise_code
```{r}
library(ggvis)
library(dplyr)

set.seed(0)

cars <- mtcars

fit <- kmeans(cars, 5)

# Aggregate your cars data by cluster fits
aggregate(cars, by=list(fit$cluster), FUN = mean)

# Create a new data frame with the cars and fit data
cluster_cars <- data.frame(cars, fit$cluster)
cluster_cars %>% ggvis(~mpg, ~disp, fill = ~factor(fit.cluster)) %>% group_by(fit.cluster)
```

*** =sct
```{r}
msg_bad <- "That is not correct, guess again."
msg_success <- "Wonderful! he 4th cluster has the best mileage."

# Pass the correct option (Action, option 2 in the instructions) to correct.
# Pass the feedback messages, both positive and negative, to feedback_msgs in the appropriate order.
test_mc(correct = 5, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_bad, msg_success)) 
```
