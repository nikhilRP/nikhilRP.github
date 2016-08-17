---
layout: post
title:  "Feature scaling and parameter tuning for SVM"
date:   2016-08-18 00:00:00
description: Feature scaling and parameter tuning for SVM
image: /assets/images/markdown.jpg
headerImage: false
tag:
- machine-learning
- svm
- scaling
blog: true
star: true
author: nikhilrp
---

Lately I have been using support vector machines a lot at work. In this blog post I am going to explain few FAQs I get about them.

### Why do we have to scale the data for SVM?

Before designing a model, its prudent to learn the characteristics of the input data. Without really understanding the data, there is no way you can design a model.

Some of the characteristics of the input data can be:

* The features maybe integers, or a combination of real and integers. (discrete versus continuous)
* Different feature may vary in size. Some features can be in low fractions while others can be very large numbers. (across features)
* Each feature by themselves may have varied values ranging from low to high. (within the feature)
* Features can be sparse (as in only some may contain values)
* Features can be dense (all of it may contain values)

Given this, its important to pre-process the input data. While all of this data is not correlated in its own, it is important in machine-learning to scale down the data to a meaningful number.

Specifically for support vector machines. SVMs make an assumption that the data provided is in a standard range, usually either 0 to 1, or -1 to 1 (roughly). So the normalization of feature vectors prior to feeding them to the SVM is very important. You want to make sure that for each dimension, the values are scaled to lie roughly within this range.

Also, if one of the features land up having a very broad range of value (Lets say a particular attribute has a value ranging from 10 to 10,000), then the rest of the distance of other variables will be governed by the particular feature (either Euclidian in case of a RBF or the vector length in case of a dot-product). In more detail, you have to normalize all of your feature vectors by dimension, not instance, prior to sending them to your SVM model.

#### Soft normalization or Zero-mean, unit-variance

You can also standardize your feature using a standard-score by determining the mean of the distribution within the range of possible values and the standard deviation. This is typically the most popular method used in other machine learning techniques such as Logistic-Regression where margins for decision-boundaries has to be calculated. The equation for Zero-mean, unit variance is as follows:

![soft-normalization]({{ site.url }}/assets/images/1-tcnp8PBqZLvXPPirjpR3VA.png)

* The subtraction of the mean from the original value (Similar to Rescaling) makes it Zero-mean.
* The division by standard deviation makes it unit variance.

Soft normalization is implemented in sklearn as preprocessing.StandardScalar

usage:

{% highlight python %}
std_scale = StandardScaler().fit(X_train)
X_train = std_scale.transform(X_train)
X_test = std_scale.transform(X_test)
{% endhighlight %}

#### Hard normalization or rescaling the feature

Rescaling the feature is a technique that sets the feature to a range between {-1, 1} based on the maximum value and the minimum value of the range within the feature. The Rescaling function is as follows:

![hard-normalization]({{ site.url }}/assets/images/1-5nKjrDASuUVKh9UpRwix6g.png)

* Here x-prime is the rescaled value
* x-bar is the average, x-max is the maximum and x-min is the minimum in the range of possible values.

Hard normalization is implemented in sklearn as preprocessing.MinMaxScalar

usage:

{% highlight python %}
std_scale = MinMaxScaler().fit(X_train)
X_train = std_scale.transform(X_train)
X_test = std_scale.transform(X_test)
{% endhighlight %}

Some libraries recommend doing a 'hard' normalization. However, in our experience, we found that is better to do a 'soft' normalization which subtracts the mean of the values and divides by twice the standard deviation (again, by dimension). Thus, if your input has d dimensions, then you will have d means and d standard deviations, no matter how many training examples you have. Note that if you're implementing this yourself, standard deviations for some dimensions might be zero, so the division could give you a divide-by-zero error. So you should add a very small epsilon value to it to prevent this.

These normalized vectors are sent to your SVM library for training. Then during testing, it is important to construct the test feature vectors in exactly the same way, except that you use the means and standard deviations saved from the training data, rather than computing it from the test data. In other words, scale your test inputs using the saved means and standard deviations, prior to sending them to your SVM.

### Parameter tuning

SVMs can be quite sensitive to training parameters, but fortunately there are relatively few of them to tune:

* C (the slack variable cost)
* γ (the width of the Gaussian if using an RBF kernel)

Generally these are searched in exponential factors: for C, something like 0.1, 1, 10, 100, 1000; for γ, something like 0.1, 0.01, 0.001, 0.0001, 0.00001). If possible, you should try all combinations of C and γ to find the ones that give you the best accuracy (using cross-validation).

If you have unbalanced input data (i.e., many more negative examples than positive), you should generally set the training weight factors for the positive and negative classes in inverse proportion, so that the trained model is not more sensitive to the class for which you have more examples. There are some circumstances where you want the training to be biased, but those are generally rare.
