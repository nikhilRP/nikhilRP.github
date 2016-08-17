---
layout: post
title:  "Feature scaling and parameter tuning for SVM"
date:   2016-08-18 00:00:00
description: Feature scaling and parameter tuning for SVM
categories:
- blog
permalink: support-vector-machines
---


Lately I have been using support vector machines a lot at work.

## Why do we have to scale the data for SVM?

Before anyone writes a model, its prudent to learn the characteristics of the input data. Without really understanding the data, there is no way you can design a model.

Some of the characteristics of the input data can be:
* The features maybe integers, or a combination of real and integers. (discrete versus continuous)
* Different feature may vary in size. Some features can be in low fractions while others can be very large numbers. (across features)
* Each feature by themselves may have varied values ranging from low to high. (within the feature)
* Features can be sparse (as in only some may contain values)
* Features can be dense (all of it may contain values)

Given this, its important to pre-process the input data. While all of this data is not correlated in its own, it is important in machine-learning to scale down the data to a meaningful number.

Specifically for support vector machines. SVMs make an assumption that the data provided is in a standard range, usually either 0 to 1, or -1 to 1 (roughly). So the normalization of feature vectors prior to feeding them to the SVM is very important. You want to make sure that for each dimension, the values are scaled to lie roughly within this range.

Also, if one of the features land up having a very broad range of value (Lets say a particular attribute has a value ranging from 10 to 10,000), then the rest of the distance of other variables will be governed by the particular feature (either Euclidian in case of a RBF or the vector length in case of a dot-product).

Its important to scale down the range of all the features so that each feature contributes proportionally to the final distance (to the vector length or some other metric)

In more detail, you have to normalize all of your feature vectors by dimension, not instance, prior to sending them to your SVM model. Some libraries recommend doing a 'hard' normalization, mapping the min and max values of a given dimension to 0 and 1. However, in our experience, we found that is better to do a 'soft' normalization which subtracts the mean of the values and divides by twice the standard deviation (again, by dimension). Thus, if your input has d dimensions, then you will have d means and d standard deviations, no matter how many training examples you have. Note that if you're implementing this yourself, standard deviations for some dimensions might be zero, so the division could give you a divide-by-zero error. So you should add a very small epsilon value to it to prevent this.

These normalized vectors are sent to your SVM library for training. Then during testing, it is important to construct the test feature vectors in exactly the same way, except that you use the means and standard deviations saved from the training data, rather than computing it from the test data. In other words, scale your test inputs using the saved means and standard deviations, prior to sending them to your SVM.

If you're using scikit-learn, then this soft scaling is provided under preprocessing.StandardScaler.

## Parameter tuning
SVMs can be quite sensitive to training parameters, but fortunately there are relatively few of them to tune:

First are C (the slack variable cost) and γ (the width of the Gaussian if using an RBF kernel) values. Generally these are searched in exponential factors: for C, something like 0.1, 1, 10, 100, 1000; for γ, something like 0.1, 0.01, 0.001, 0.0001, 0.00001). If possible, you should try all combinations of C and γ to find the ones that give you the best accuracy (using cross-validation). Also, if you're competing for a benchmark, it's important you evaluate this on a held out subset so you don't inadvertently overfit to the benchmark data.

If you have unbalanced input data (i.e., many more negative examples than positive), you should generally set the training weight factors for the positive and negative classes in inverse proportion, so that the trained model is not more sensitive to the class for which you have more examples. There are some circumstances where you want the training to be biased, but those are generally rare.
