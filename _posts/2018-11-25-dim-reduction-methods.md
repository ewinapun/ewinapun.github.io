---
layout: post
title: Differences Between Various Dimension Reduction Techniques
date: 2018-11-25 06:00
description: Let's talk about linear dimension reduction techniques.
published: true
---

Imagine this scenerio: you getting late for a party, but you completely forget where you left your keys in your messy room (I get it, a typical college student room) and took way longer than needed to find it ~~anyways you're late to begin with~~. Frustrating isn't it? Wouldn't it be much easier to find it if your room is unclustered and neat? ~~dah that's what your mom has been trying to say.~~

Now apply this mindset to data analysis, That is why we perform dimension reduction.


Feature projection transforms the data in the high-dimensional space to a space of fewer dimensions.

# Linear Discriminant Analysis

\href{http://sebastianraschka.com/Articles/2014_python_lda}{[Raschka]}. It projects a dataset onto a lower-dimensional space with good class-separability in order to avoid overfitting (“curse of dimensionality”) and reduce computational costs. LDA is “supervised” and computes the directions (“linear discriminants”) that will represent the axes that 1) maximize the distance between means/ find a the central point with maximum distances from means 2) minimize the variances ("scatters") within each category; in math terms, it maximizes $$\sum{d_i^2}/\sum{s_i^2}$$ where $$d_i$$ represents distances and $$s_i$$ represents variances of the $$i$$\textsuperscript{th} category.

# Principle Component Analysis

But it's goal is to find the axes ("principle components") with maximum variance for the whole data set. Adopted from \href{https://www.youtube.com/watch?v=FgakZw6K1QQ}{[StatQuest]}, we can calculate the main principle components, namely PC1, by first recenter the dataset according to the means of the variables. PC1 is a line that passes though the origin and maximizes the distances of the projected data points from the origin. The sum of squared distances of the data set from the ) is the "eigenvalue" for PC1; square root of the eigenvalue is the "singular value"; divide it by $$n-1$$ is the "variation"; "singular vector" or "eigenvector" is a unit vector of PC1. The other principle components are the perpendicular axes of PC1. With these new axes, data are presented using the projections on each PC. Each PC has a corresponding variation. Same idea as SVD, The PCs that account a smaller portion of the total variation provides less information about the dataset, and thus can be discarded to reduce the dimensionality.


PCA | LDA | FA |
