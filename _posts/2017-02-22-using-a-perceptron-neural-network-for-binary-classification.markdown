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
tldr; can we use a perceptron neural network to improve out application or infrastructure monitoring e.g. determine erroneous alerts or adjust our alerting thresholds automatically based on past events?

In this blog post, I will discuss my adventures implementing a binary classifier, for linearly separable data using an artificial neural network (ANN).

A neural network can be considered as a network of nodes connected by weights that takes 'n' number of inputs. See figure 1. To calculate the output of the neural network you multiply all the network inputs by their weights, sum them and pass them to an activation function which determines the output of the network. This is classification.

[![Figure 1: Perceptron Artificial Neural Network](https://robertnorthard.com/assets/images/2017-07-22-perceptron-neural-network.png "Perceptron Artificial Neural Network")](https://robertnorthard.com/assets/images/2017-07-22-perceptron-neural-network.png "Perceptron Artificial Neural Network")

The inputs to the neural network can be considered the features or attributes of the object to classify. In our case, we will solve a simple problem. The logical 'AND' operator (Figure 2 truth table) as it is well-defined and involves two binary inputs.

|Input 1| Input 1| Expected Output |
|-------|--------|---------|
| 1 | 1 | 1 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 0 |

To train the neural network we adjust the weights. Will we use the <a href="https://en.wikipedia.org/wiki/Perceptron">Perceptron</a> <a href="https://en.wikipedia.org/wiki/Supervised_learning">supervised learning method</a> to train the network. This means for any two inputs we know what the expected output is and that as the algorithm is applied through a number of iterations which are called epoch the network converges towards a solution. This truth table above is the training set to be used by the Perceptron algorithm.

First, we need to define our <a href="https://en.wikipedia.org/wiki/Activation_function">activation function</a> for calculating the output of the network. We will say if the sum of the inputs multiplied by their weights is more than 0.5 the network will output a 1, else 0. This is referred to as a <a href="http://www.intmath.com/laplace-transformation/1a-unit-step-functions-definition.php">unit step function</a>.

To train the network will we do the following:
<ol>
 	<li>Set the current weights of the network to random numbers.</li>
 	<li>For each training set calculate the error by taking the expected result from the actual and adjust the weights accordingly by some percentage which is defined as the learning rate.</li>
 	<li>Repeat steps 2 for 'n' epoch until the solution is solved. Not all solution are solvable with this network setup. Try XOR.</li>
</ol>
By doing this we can see that by setting all the weights to 0.2 it will solve the logical AND problem.

e.g.
Input 1 = 1
Input 2 = 1
Bias = 1
output = (1 * 0.2) + (1*0.2) + (1*0.2) = 0.6 &gt; 0.5 = 1

<strong>Whats next?</strong>
<ul>
 	<li>Can we use this in our application or infrastructure monitoring to determine erroneous alerts or adjust our alerting thresholds automatically based on past events?</li>
</ul>

See a Python implementation of this network [here](https://github.com/RobertNorthard/perceptron-artificial-neural-network "Python implementation of Perceptron ANN").
