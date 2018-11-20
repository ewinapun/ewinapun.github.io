---
layout: post
title: Differences Between Various Dimension Reduction Methods
date: 2018-11-25 06:00
description: PCA, LDA, factoral analysis, and more to talk about.
published: false
---

# Linear Discriminant Analysis

\href{http://sebastianraschka.com/Articles/2014_python_lda}{[Raschka]}. It projects a dataset onto a lower-dimensional space with good class-separability in order to avoid overfitting (“curse of dimensionality”) and reduce computational costs. LDA is “supervised” and computes the directions (“linear discriminants”) that will represent the axes that 1) maximize the distance between means/ find a the central point with maximum distances from means 2) minimize the variances ("scatters") within each category; in math terms, it maximizes $$\sum{d_i^2}/\sum{s_i^2}$$ where $$d_i$$ represents distances and $$s_i$$ represents variances of the $$i$$\textsuperscript{th} category.

# Principle Component Analysis

But it's goal is to find the axes ("principle components") with maximum variance for the whole data set. Adopted from \href{https://www.youtube.com/watch?v=FgakZw6K1QQ}{[StatQuest]}, we can calculate the main principle components, namely PC1, by first recenter the dataset according to the means of the variables. PC1 is a line that passes though the origin and maximizes the distances of the projected data points from the origin. The sum of squared distances of the data set from the ) is the "eigenvalue" for PC1; square root of the eigenvalue is the "singular value"; divide it by $$n-1$$ is the "variation"; "singular vector" or "eigenvector" is a unit vector of PC1. The other principle components are the perpendicular axes of PC1. With these new axes, data are presented using the projections on each PC. Each PC has a corresponding variation. Same idea as SVD, The PCs that account a smaller portion of the total variation provides less information about the dataset, and thus can be discarded to reduce the dimensionality.
