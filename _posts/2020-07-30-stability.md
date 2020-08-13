---
layout: post
title: Neural Nonstationarity During Stable Movement Control
date: 2020-07-30 06:00
description: What is nonstationarity, and how scientists deal with it
published: false
---


Dickey et al. proposed a criterion to assess single-unit stability by measuring the similratiy of spike sorted neuron's average spike waveforms and interspike interval histograms (ISIHs)

Kim et al. proposed assessing stability on an ensemble level by estimating a multivariate Gaussian distribution at different time periods and measure the KL divergence between the distributions.

# Unsupervised methods
Let the data speak for itself
Unsupervised methods that don’t put in any information about the task can thus lead to more persuasive and potentially more surprising results.

# Latent Manifold

data with nontrivial structure

Dimensionality reduction “places more emphasis on recovering coordinates for points that lie on the manifold; manifold discovery suggests additional interest in the structure of the manifold itself,” says Ryan Low, a research fellow at University College London.

## spline parameterization for unsupervised decoding (SPUD)
Rishidev Chaudhuri Nature Neuroscience in August

SPUD, on neural activity in the anterodorsal thalamic nucleus (ADN), a region that houses neurons known to encode head direction.

‘manifold discovery,’ a way to characterize and understand the lower-dimensional topology that exists in high-dimensional data.

SPUD starts by placing the activity of individual neurons on separate axes in a high-dimensional space, creating a point cloud of data. The shape of that point cloud is then characterized using a technique called persistent homology, which determines which features of the shape remain as the resolution of the data is changed. Using this knowledge about the data’s shape, researchers calculate its intrinsic dimensionality and fit a function to it. The benefit of fitting this function is that it provides a simple way to describe a given data point’s location on the manifold.

Using this method, they found that the activity of the ADN neurons recorded while the animal explored an open environment falls largely along a one-dimensional ring. What’s more, the population activity’s location on this ring at any moment could be used to predict the heading direction of the animal with high accuracy, despite the fact that information about heading direction is never used as part of the analysis method. Thus, this unsupervised analysis of the neural data successfully uncovered the relevant information represented by the population.

## manifold inference from neural dynamics (MIND)

Ryan Low BioAxiv 2018

defines the distance between two patterns of neural activity as a function of how the network transitions between the patterns over time

recorded activity from the CA1 region of the hippocampus as rodents foraged in a 2D space or performed a sound manipulation task in 1D frequency space

neural activity during the 2D foraging task was well captured by three dimensions, and during the 1D auditory task it was well captured by two dimensions.

the extra dimension is unlikely to be just noise as they should show up across many dimensions

## Gaussian process latent variable model (GPLVM) (Anqi Wu, et al., 2018)
http://pillowlab.princeton.edu/pubs/Wu18_NeurIPS_LatentOlfactoryManifold.pdf

analyze activity in the olfactory cortex, where the relationship between the physical properties of odor molecules and the neural representations they elicit has never been clear.
GPLVM aims to identify a latent manifold on which large changes in neural responses to odor can be seamlessly related to each other and hopefully related back to properties of the odor.
Specifically, the activity of each neuron can be explained as a nonlinear function of the latent variables the model identifies, along with a noise term.
With this method, researchers can predict the response of part of the population to a new odor by using the response of the rest of the population to determine the odor’s location in the latent space.
Following this technique, the team was able to capture a large portion of the single-trial responses to new odors in the mouse piriform cortex.
they found that the activity of many hundreds of piriform neurons can be represented by 10 to 15 latent dimensions.
