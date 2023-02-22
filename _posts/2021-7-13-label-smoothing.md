---
title: 标签平滑技术（Label Smoothing）
tags:
  - Classification
  - Overfitting
  - Overconfidence
---
This article is a repost from the [What is Label Smoothing?](https://towardsdatascience.com/what-is-label-smoothing-108debd7ef06.)

When using deep learning models for classification tasks, we usually encounter the following problems: overfitting, and overconfidence. Overfitting is well studied and can be tackled with early stopping, dropout, weight regularization etc. On the other hand, we have less tools to tackle overconfidence. Label smoothing is a regularization technique that addresses both problems.

## Overconfidence and Calibration

A classification model is calibrated if its predicted probabilities of outcomes reflect their accuracy. For example, consider 100 examples within our dataset, each with predicted probability 0.9 by our model. If our model is calibrated, then 90 examples should be classified correctly. Similarly, among another 100 examples with predicted probabilities 0.6, we would expect only 60 examples being correctly classified.

Model calibration is important for

- model interpretability and reliability
- deciding decision thresholds for downstream applications
- integrating our model into an ensemble or a machine learning pipeline

An overconfident model is not calibrated and its predicted probabilities are consistently higher than the accuracy. For example, it may predict 0.9 for inputs where the accuracy is only 0.6. Notice that models with small test errors can still be overconfident, and therefore can benefit from label smoothing.


## Formula of Label Smoothing

Label smoothing replaces one-hot encoded label vector y_hot with a mixture of y_hot and the uniform distribution:

> y_ls = (1 - α) * y_hot + α / K

where K is the number of label classes, and α is a hyperparameter that determines the amount of smoothing. If α = 0, we obtain the original one-hot encoded y_hot. If α = 1, we get the uniform distribution.

## Motivation of Label Smoothing

Label smoothing is used when the loss function is cross entropy, and the model applies the softmax function to the penultimate layer’s logit vectors z to compute its output probabilities p. In this setting, the gradient of the cross entropy loss function with respect to the logits is simply

> ∇CE = p - y = softmax(z) - y

where y is the label distribution. In particular, we can see that

1. Gradient descent will try to make p as close to y as possible.
2. The gradient is bounded between -1 and 1.

One-hot encoded labels encourages largest possible logit gaps to be fed into the softmax function. Intuitively, large logit gaps combined with the bounded gradient will make the model less adaptive and too confident about its predictions.

In contrast, smoothed labels encourages small logit gaps, as demonstrated by the example below. It is shown in [3] that this results in better model calibration and prevents overconfident predictions.

## A Concrete Example

Suppose we have K = 3 classes, and our label belongs to the 1st class. Let [a, b, c] be our logit vector.

If we do not use label smoothing, the label vector is the one-hot encoded vector [1, 0, 0]. Our model will make a ≫ b and a ≫ c. For example, applying softmax to the logit vector [10, 0, 0] gives [0.9999, 0, 0] rounded to 4 decimal places.

If we use label smoothing with α = 0.1, the smoothed label vector ≈ [0.9333, 0.0333, 0.0333]. The logit vector [3.3322, 0, 0] approximates the smoothed label vector to 4 decimal places after softmax, and it has a smaller gap. This is why we call label smoothing a regularization technique as it restrains the largest logit from becoming much bigger than the rest.

## Implementation

- Tensorflow: Label smoothing is already implemented in Tensorflow within the cross entropy loss functions. See e.g BinaryCrossentropy and CategoricalCrossentropy.
- PyTorch: See the example from OpenNMT.

## Frequently Asked Questions

Q: When do we use label smoothing?

A: Whenever a classification neural network suffers from overfitting and/or overconfidence, we can try label smoothing.

Q: How do we choose α?

A: Just like other regularization hyperparameters, there is no formula for choosing α. It is usually done by trial and error, and α = 0.1 is a good place to start.

Q: Can we use distributions other than uniform distribution in label smoothing?

A: Technically yes. In [4] the theoretical groundwork is developed for arbitrary distributions. That being said, the vast majority of empirical studies on label smoothing use uniform distribution.

Q: Is label smoothing used outside deep learning?

A: Not really. Most popular non-deep learning methods do not use the softmax function. Thus label smoothing is usually not applicable.

Further Reading
1. [3] studies how and why label smoothing works, provides a new visualization scheme, and analyzes the performance of label smoothing for different tasks. The section of Knowledge Distillation is especially interesting.
2. [5] and [4] discuss how label smoothing affects the loss function and also its connection to KL divergence.
3. [1] Chapter 7.5.1 covers how label smoothing helps dealing with noisy labels.
4. [2] introduces temperature scaling which is a simple yet effective way to calibrate a neural network.

## References
1. I. Goodfellow, Y. Bengio, and A. Courville. Deep Learning (2016), MIT Press.
2. C. Guo, G. Pleiss, Y. Sun, and K. Weinberger. On Calibration of Modern Neural Networks (2017), ICML 2017.
3. R. Müller, S. Kornblith, and G. Hinton. When Does Label Smoothing Help? (2019), NeurIPS 2019.
4. G. Pereyra, G. Tucker, J. Chorowski, Ł. Kaiser, and G. Hinton. Regularizing Neural Networks by Penalizing Confident Output Distributions (2017), arXiv.
4. C. Szegedy, V. Vanhoucke, S. Ioffe, J. Shlens, and Z. Wojna. Rethinking the Inception Architecture for Computer Vision (2016), CVPR 2016.