---
layout: post
title: Guide to Various Dimension Reduction Techniques
date: 2018-11-25 06:00
description: Let's talk about linear dimension reduction techniques.
published: true
---

Imagine this scenerio: you are getting late for a movie, but you forget where you left your keys in your messy room. You ended up taking way longer than needed to find them. Frustrating isn't it? Wouldn't it be much easier if your room were clean and organized?

Now apply this thinking to your data, is there a way to "*tidy up*" the data prior to any regression or classification, so that some features can be easier to observe? Indeed dimension reduction is what we need. Dimension reduction offers a reduction of time and storage space required, and it allows us to easily visualize the data through projecting data in higher-dimensional space to lower-dimensional space.

I will cover three major linear dimensionality reduction techniques, namely Principle Component Analysis (PCA), Linear Discriminant Analysis (LDA), and Factor Analysis (FA).

## What is feature projection?

![Chernin Entertainment Logo obtained from http://logos.wikia.com/wiki/Chernin_Entertainment/Other](/assets/img/posts/CE.png)


# Linear Discriminant Analysis

It projects a dataset onto a lower-dimensional space with good class-separability in order to avoid overfitting (“curse of dimensionality”) and reduce computational costs. LDA is “supervised” and computes the directions (“linear discriminants”) that will represent the axes that 1) maximize the distance between means/ find a the central point with maximum distances from means 2) minimize the variances ("scatters") within each category; in math terms, it maximizes $$\sum{d_i^2}/\sum{s_i^2}$$ where $$d_i$$ represents distances and $$s_i$$ represents variances of the $$i$$\textsuperscript{th} category.

# Principle Component Analysis

But it's goal is to find the axes ("principle components") with maximum variance for the whole data set. Adopted from \href{https://www.youtube.com/watch?v=FgakZw6K1QQ}{[StatQuest]}, we can calculate the main principle components, namely PC1, by first recenter the dataset according to the means of the variables. PC1 is a line that passes though the origin and maximizes the distances of the projected data points from the origin. The sum of squared distances of the data set from the ) is the "eigenvalue" for PC1; square root of the eigenvalue is the "singular value"; divide it by $$n-1$$ is the "variation"; "singular vector" or "eigenvector" is a unit vector of PC1. The other principle components are the perpendicular axes of PC1. With these new axes, data are presented using the projections on each PC. Each PC has a corresponding variation. Same idea as SVD, The PCs that account a smaller portion of the total variation provides less information about the dataset, and thus can be discarded to reduce the dimensionality.

In factor analysis we model the observed variables as linear functions of the “factors.” In principal components, we create new variables that are linear combinations of the observed variables.

## Summary table

| PCA | LDA | FA |
| find component axes that maximize the variance of our data | find component axes that maximize the separation between multiple classes
| unsupervised | supervised
