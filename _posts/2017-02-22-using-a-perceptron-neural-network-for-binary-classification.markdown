---
title: "Using a Perceptron Neural Network for Binary Classification"
layout: post
date: 2017-07-22 23:22
headerImage: false
tag:
- Artificial Neural Network
- Artificial Intelligence
- Perceptron
star: false
category: blog
author: robertnorthard
description: Using a Perceptron Neural Network for Binary Classification
---

In this blog post, I will discuss my adventures implementing a binary classifier, for linearly separable data using the Perceptron Artificial Neural Network (ANN).

[![Figure 1: Perceptron Artificial Neural Network](https://robertnorthard.com/assets/images/2017-07-22-perceptron-neural-network.png "Perceptron Artificial Neural Network")](https://robertnorthard.com/assets/images/2017-07-22-perceptron-neural-network.png "Perceptron Artificial Neural Network")

A neural network can be considered as a network of nodes connected by weights that takes 'n' number of inputs. See figure 1. To calculate the output of the neural network we multiply all the network inputs by their weights, sum them and pass them to an activation function which determines the output of the network. This is classification.

The inputs to the neural network can be considered the features or attributes of the object to classify. In our case, we will solve a simple problem, the logical 'AND' operator (Figure 2 truth table) as it is well-defined and involves two binary inputs.

|Input 1| Input 1| Expected Output |
|-------|--------|---------|
| 1 | 1 | 1 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 0 |

To train the neural network we adjust the network weights. The weights can be defined as a vector. There are various algorithm to do this but we will use gradient descent which is a supervised learning algorithm. This means for any two inputs we know what the expected output is and that as the algorithm is applied through a number of iterations which are called epoch the network converges towards a solution. This truth table above is the network's training set.

First, we need to define our activation function for classification. We will say if the sum of the inputs multiplied by their weights is more than 0.5 the network will output a 1, else 0. This is referred to as a unit step function.

To train the network will we do the following:

1. Set the current weights of the network to random numbers.
2. For each row in the training set calculate the error by taking the expected result from the actual and adjust the weights accordingly by some percentage which is defined as the learning rate.
3. Repeat steps 2 for 'n' epoch until the solution is solved. This network will not solve every problem. How would you solve it for the 'XOR' operator?

By doing this we can see that by setting all the weights to 0.2 it will solve the logical AND problem.

e.g.
* Input 1 = 1
* Input 2 = 1
* Bias = 1 (always equals 1)
* output = (1 * 0.2) + (1 * 0.2) + (1 * 0.2) = 0.6 > 0.5 = 1

See a Python implementation of this network [here](https://github.com/RobertNorthard/perceptron-artificial-neural-network "Python implementation of Perceptron ANN").