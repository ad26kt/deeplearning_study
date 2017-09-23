# Batch Normalization

> Refer to : [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift]

## Abstract
Training Deep Neural Networks is complicated by the fact that the **distribution of each layer’s inputs changes during training**, as the parameters of the previous layers change. This **slows down the training** by requiring lower learning rates and careful parameter initialization, and makes it notoriously hard to train models with saturating nonlinearities. We refer to this phenomenon as ***internal covariate shift***, and address the problem by normalizing layer inputs. Our method draws its strength from making normalization a part of the model architecture and performing the normalization for each training mini-batch. Batch Normalization **allows us to use much higher learning rates and be less careful about initialization**. It also acts as a regularizer, in some cases **eliminating the need for Dropout**. Applied to a state-of-the-art image classification model, Batch Normalization achieves the same accuracy with 14 times fewer training steps, and beats the original model by a significant margin. Using an ensemble of batchnormalized networks, we improve upon the best published result on ImageNet classification: reaching 4.9% top-5 validation error (and 4.8% test error), exceeding the accuracy of human raters.

## Introduction
SGD(stochastic gradient descent) is a kind of very fundamental training algorithm in Deep Learning.

Using mini-batches of examples, as opposed to one example at a time, is helpful in several ways.
- The gradient of the loss over a mini-batch is an estimate of the gradient over the training set, whose quality improves as the batch size increases
- Computation over a batch can be much more efficient than m computations for individual examples

Carefulness required by GD : tuning parameters such as learning rate and initial values

Continuous change in the distribution of layer's input presents a problem because the layers need to continuously adapt to the new distribution. When the input distribution to a learning system changes, it is said to experience covariate shift (Shimodaira, 2000).

Arbitrary two-layer network function: $$F_{\theta_2}(F_{\theta_1}(x))$$
x is an input to the network
we can treat output of the inner network $$u = F_{\theta_1}(x)$$ as an input to the outer network $$F_{\theta_2}(u)$$
Input distribution properties that make training efficient( such as having same train/test distribution) can also be applied to the sub-network

Consider a layer with sigmoid activation function : $$output = f(Wx + b)$$
we know that when $$|u|$$ gets bigger, $$f'(u)$$ tends to zero. For all dimention of u, the gradient flowing down to x will vanish and make training slower except for those with small absolute value. $$u$$ is affected by $$W, b$$ and the parameters of lower layers, changes to those parameters during training will likely move many dimensions of $$u$$ into the saturated regime of the nonlinearity and slow down the convergence. This effect is amplified as the network depth increases.***( I don't understand here )***

**Internal Covariance Shift** : Change in distribution of internal layers in deep network.

**Batch Normalization** : A normalization step that fix the means and variances of layer input
-- reduce the dependence of gradient on the scale of parameters or their initial values
-- make training faster, prevent from getting stuck in saturated modes
-- can alternate dropout





 




[//]: # (These are reference links used in the body of this note)
[Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift]: <https://arxiv.org/pdf/1502.03167.pdf>
