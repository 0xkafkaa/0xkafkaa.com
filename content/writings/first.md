+++
title = "On the Mathematics of Learning"
date = 2026-10-14
description = "A short exploration of gradients, optimization, and the mathematics behind machine learning."
+++

# On the Mathematics of Learning

_Notes on calculus, optimization, and machine learning._

Mathematics is not merely a collection of formulas. It is a language for describing patterns, relationships, and change. In machine learning, this language becomes particularly useful when we attempt to understand how a model learns from data.

## 1. The Idea of Change

Consider a simple function:

$$
f(x) = x^2
$$

Its derivative is:

$$
f'(x) = 2x
$$

The derivative tells us how rapidly the function changes at a particular point.

For instance, at $x = 3$, the slope of the tangent line is $6$.

This simple observation forms the foundation of optimization.

## 2. From Derivatives to Gradients

When a function depends on several variables, we use partial derivatives.

Consider:

$$
f(x,y) = x^2 + y^2
$$

The gradient is the vector of partial derivatives:

$$
\nabla f(x,y) =
\begin{bmatrix}
2x \\
2y
\end{bmatrix}
$$

The gradient points in the direction of steepest local increase.

To minimize a differentiable function, we can move in the opposite direction.

> The gradient tells us which direction increases the function most rapidly. The negative gradient gives us a direction of local decrease.

## 3. Gradient Descent

Gradient descent is an iterative optimization algorithm.

Its update rule is:

$$
\theta_{t+1} = \theta_t - \eta \nabla L(\theta_t)
$$

Here:

- $\theta$ represents the model parameters.
- $\eta$ represents the learning rate.
- $L$ represents the loss function.
- $\nabla L$ represents the gradient of the loss.

The learning rate determines how large each step will be.

### Choosing a Learning Rate

A learning rate that is too large may cause the optimization process to diverge.

A learning rate that is too small may make convergence extremely slow.

Finding an appropriate learning rate is therefore an important part of training a model.

## 4. Implementing Gradient Descent

The following Python example minimizes a simple quadratic function.

```python
def gradient(x):
    return 2 * x

def gradient_descent(x, learning_rate=0.1, steps=100):
    for _ in range(steps):
        x = x - learning_rate * gradient(x)
    return x

result = gradient_descent(10)

print(result)
```

The algorithm gradually approaches the minimum at $x = 0$.

## 5. Questions Worth Exploring

Several questions naturally arise from this discussion:

1. Why does the negative gradient indicate a direction of decrease?
2. What happens when the loss function has multiple local minima?
3. How does gradient descent behave in higher dimensions?
4. Why do neural networks require backpropagation?
5. How do second derivatives help us understand optimization?

These questions lead us toward more advanced topics in numerical optimization and deep learning.

## 6. Further Reading

For a deeper understanding of these concepts, the following resources are useful:

- [Mathematics for Machine Learning](https://mml-book.github.io/)
- [Deep Learning — Ian Goodfellow et al.](https://www.deeplearningbook.org/)
- [3Blue1Brown — Essence of Calculus](https://www.3blue1brown.com/topics/calculus)

---

_Learning mathematics is not about memorizing formulas. It is about developing an intuition for why those formulas work._
