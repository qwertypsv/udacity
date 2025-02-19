ud120-projects
==============

Starter project code for students taking Udacity ud120


Since my system was showing memory error for given test size = 0.1, so I used test size from a range of values from 0.1 to 0.5. But when I sliced the data I was able to run using given test_size=0.1*

In order to change test _size go to *'/machine-learning-project/tools/email_preprocess.py'*

Given test_size = 0.1, Current test_size = 0.2. Most of the time I will be using test_size *0.2*. In below screenshots, no. of Chris & Sara's training emails are prior to slicing.

***
    
### Enron Data set
 * Analysis 
 
    ![Output](https://github.com/p-s-vishnu/udacity/blob/master/machine-learning-project/images/enron_analysis.PNG)
    
    * Not every POI has an entry in the dataset (e.g. Michael Krautz)
    * That’s because the dataset was created using the financial data you can find in final_project/enron61702insiderpay.pdf, which is missing some POI’s (that absence propagated to the final dataset)
    * On the other hand, for many of these “missing” POI’s, we do have emails
    * If you added in, say, 10 more data points which were all POI’s, and put “NaN” for the total payments for those folks, the numbers you just calculated would change
    * But adding in the new POI’s in this example, none of whom we have financial information for, has introduced a subtle problem, that our lack of financial information about them can be picked up by an algorithm as a clue that they’re POIs

*** 

### Supervised Classification Algorithms
The below observations are part of mini-project, email author identifier 

### Algorithm 1 : Naive Bayes

![Output](https://github.com/p-s-vishnu/udacity/blob/master/machine-learning-project/images/NaiveBayes.PNG)

**Disadvantage** : It makes a very strong assumption on the shape of your data distribution, i.e. any two features are independent given the output class. E.g In a sentence, the algorithm doesn't consider the sequence of words, instead it focuses only on the number of words that appear in the sentence.

### Algorithm 2 : SVM (Support Vector Machine)
##### Speed - Accuracy tradeoff 
* SVM is MUCH slower to train and use for predicting

	![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM.PNG)

* Trained using a smaller training set (1% of test_size)

	![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_small.PNG)

* Using the above sliced training set, I trained using *kernel as 'rbf'*

	![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_small_rbf.PNG)

* In the above case, varied the C values to 10, 100, 1000, 10000 (with test_size = 0.1). *As the value of C increased Accuracy also increased* 

	![10](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_10.PNG)

	![100](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_100.PNG)

	![1000](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_1000.PNG)

	![10000](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_10000.PNG)

* Removing the slicing and re-training with the C = 10000 and test_size = 0.11 (since 0.1 shows memory errors)

	![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_rbf.PNG)

* The author of 10th, 26th and 50th mail

	![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/SVM_prediction.PNG)

* The total number of mails which belonged to Chris(1) were *877* (with test_size = 0.1, no slicing, accuracy of 99%) 

**Advantage** :
+ It performs well where there is a clear separation 

**Disadvantage**:
- Low performance in large data set
- If the data is having more noise, Naive Bayes has the upper hand

### Algorithm 3 : Decision Trees

* min_samples_split = 40

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/DT_min_40.PNG)
    
* Number of features = 3785
* In order to reduce the complexity of Tree, the number of features can be modified(feature selection).
Here sklearn.feature_selection.SelectPercentile's parameter(percentile) can be modified to reduce features.
* Accuracy of decision tree while using only 1% of available features = 97%

### Algorithm 4 : KNN

*   Input of terrain  data set

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/input.png)
*   parameter, n_neighbors=3

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/KNN_output.png)
*   Accuracy with 3 n_neighbour is 93.6 %

### Algorithm 5 : Adaboost
*   Accuracy : 92.4 %

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/Adaboost_output.png)

### Algorithm 6 : Random forest 
**Advantage** :
*   Won't overfit the model.
*   Handles data with missing data and maintains accuracy 
*   Large data set with higher dimensionality handled well

**Disadvantage** :
*   Not high accuracy for Regression problems.
*   Little control over what the model does.

*   Accuracy : 93.6 %

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/random_forest_output.png)

***
### Supervised Regression Algorithms
 
**Discrete v/s continuous classifier**
*   The definition of discrete is: individually separate and distinct. eg : Time is continuous.
*   Sometimes the way we define the problem makes it discrete or continuous. 
E.g : Weather is the given amount of light that reaches the ground in a period of time. But if we consider 
whether the weather is sunny or rainy, it can be defined as a discrete problem.
* Continuous will have sort of ordering.

### Algorithm 1 : Linear regression (Uni variate and multivariate)

* Evaluation of Line can be done through Error = Actual value - Predicted value
* A good fit to minimize, 
    * Sum of Absolute value of errors 
    * Sum of square of error
* Some algorithms to minimize sum of square of error
    * Ordinary least squares (Used in sklearn)
    * Gradient descent  
* Why sum of square of error considered and not Absolute value?
   
    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/min_sum_sq_errors.PNG)
* Sum of square error is not perfect, even though the regression line might be doing a good job but as the number of 
data points increase the sum of square increases. Hence while comparing two similar distribution, the one with larger
number of data points will be considered worse.

* R-squared error is not facing the above shortcoming, is very good *evaluation metric*

* R-square can be described as "how much of my change in output(y) is explained by input(x)". Value range from 0 to 1.
Capturing trend in in data. *Important* it is independent of the number of training point. 

* Back to Enron Data set, predicting bonus w.r.t salary.
 
* The score was better when tried to predict bonus w.r.t long term incentive, hence that is a strong feature

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/regression_input.png)

***

### Outliers
* What causes outliers ?
    * Sensor malfunction
    * Incorrect data entry
    * Freak events
    
* Outlier detection and removal
    1. Initially train the model.
    2. Remove the point with larger Residual error (10% of data points)
    3. Retrain, repeat step ii and iii 

* Outlier detection using Residual error, residual error is the error the data point has once you fit the best possible line.

* Before removing outlier (age vs the net worth of person)

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/age_networth_with_outlier.png)
* After removing 10% of data points (points with top 10% Residual error). Remaining 81 data points. 
    
    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/age_networth_without_outlier.png)
* Observations

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/outlier_cleaner.PNG)
    * There was a spreadsheet quirk in the data set, TOTAL was considered as a KEY with Max Salary=26704229
    
    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/enron_outlier_total.png)
    * After removing the key 'TOTAL'
    
    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/enron_outlier_removed.png)

***

### Unsupervised Learning Algorithms
### Clustering (K means clustering only discussed)
*   Algorithm
    1. Assign cluster centers
    2. Optimize cluster centers (until no change)
* The problem with k-means is the final cluster is proportional to the initial random point.
* Some useful parameters - n_clusters, n_init (number of random initialization to avoid the above problem) and max_iter.
* This is a local hill climbing algorithm, hence it is possible to get stuck in a local minimum.
* Other types of clustering - Hierarchical clustering and Probabilistic clustering (Fuzzy k means)  
* Enron dataset, Initial input

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/k_means_input.png)
* Clusters with 2 features, 'salary' and 'exercised_stock_options'

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/k_means_2_features.png)
* Clustering with an additional feature 'total_payments'

    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/k_means_3_features.png)
    
### Feature scaling

* It is the method of normalizing features, so that one or few features may not dominate the result. The features will still
 represent their original nature but now be expressed in a much smaller range. Below is a min-max rescaler
 
    ![Output](https://github.com/qwertypsv/udacity/blob/master/machine-learning-project/images/featurescale_formula.png)
* Out of decision trees, svm with rbf kernel, linear regression and k-means which of these will be affected by *feature scaling*?
    
    Ans : svm with rbf and k-means.    
