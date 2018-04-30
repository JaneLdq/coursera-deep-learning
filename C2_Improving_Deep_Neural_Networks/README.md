# Course 2 - Improving Deep Neural Networks
Hyperparameter tuning, Regularization and Optimization

## Setting up Machine Learning Application
* Train / Dev / Test sets
    * Common practice: 70/30/ . or 60/20/ 20
    * Big data: 98/1/1


* Bias / Variance

Example | High Variance | High Bias | High Variance & High Bias | Low Bias & Low Variance
|---|---|---|---|---
Training Set Error | 1% | 15% | 15% |0.%
Dev Set Error | 11% | 16% | 30% | 1%

* Basic Recipe for Machine Learning

![Basic Recipe for machine learning](images/basic-recipe-for-ml.png)

## Regularizing - prevent overfitting

* L2/Frobenius Regularization (hyper parameter: λ = regularization paramter)
* L1 Regluarization (less common)
* Dropout Regularization
* Data augmentation
* Early Stopping


## Optimization
* Normalizing inputs
* Weight Initialization: partially solve Vanishing/Exploding gradients problem
    * Xavier initialization
    * ...
* Gradient checking: using numerical approximation of gradients
    * Don't use in training - only to debug, it is much too slow
    * If algorithm fails grad check, look at components to try to identify bug
    * Remember regularization
    * Doesn't work with dropout
    * Run at random initialization; perhaps again after some training

### Optimization Algorithms
#### Mini-batch gradient descent
Use Batch with large data is too slow because for each gradient descent step you need go through the whole data set


Mini-batch Size | Gradient Descent | Optimizing Cost Function | Tips
---|---|---|---
1 | Stochastic Graient Descent (every example is its own mini-batch) <br> (X<sup>{1}</sup>, Y<sup>{1}</sup>) = (X<sup>(1)</sup>, Y<sup>(1)</sup>) <br>(X<sup>{2}</sup>, Y<sup>{2}</sup>) = (X<sup>(2)</sup>, Y<sup>(2)</sup>) ... | extremely noisy, won't ever converge<br>*lose speed up from vectorization* |
(1, m) | Mini-batch Gradient Descent | In practice, fartest learning<br>1. vectiorization, <br>2. make progress without procesing entire training set | 1. Typical mini-batch size: 64, 128, 256, ... <br>2. Make sure mini-batch fits in CPU/GPU memory
m | Batch Gradient Descent - (X<sup>{1}</sup>, Y<sup>{1}</sup>) = (X, Y) | low noise, large steps, <br>*too long per iteration* | Use Batch if training set is small, m <= 2000

#### Bias Correction
Bias correction in exponentially weighted averages - during the initial phase of learning when warming up the estimates the bias correction can help to obtain a better estimate

#### Gradient descent with Momentum
The basic idea is to compute an exponentially weighted average of your gradients, and then use that gradient to update your weights instead.

*For iteration t, compute dW, db using current mini-batch and then do gradient descent as formula shown below:*

![momentum_vdw_vdb](images/momentum_vdw_vdb.gif) <br>![momentum_w_b](images/momentum_w_b.gif)

* **Hyperparameters**: α(learning rate), β = 0.9

#### RMSprop

*For iteration t, compute dW, db using current mini-batch and then do gradient descent as formula shown below:*

![rms_sdW_sdb](images/rms_sdW_sdb.gif) <br> ![rms_W_b](images/rms_w_b.gif)

* **epsilon** is used to prevent the denominator to be zero

#### Adam optimization algorithm

*Initialize v<sub>dW</sub>=0, S<sub>dW</sub>=0, v<sub>db</sub>=0, S<sub>db</sub>=0, <br>For iteration t, compute dW, db using current mini-batch and then do the gradient descent as formula shown below:*

![adam_momentum_vdw_vdb](images/adam_momentum_vdw_vdb.gif) <br> ![adam_rms_sdw_sdb](images/adam_rms_sdw_sdb.gif) <br> ![adam_momentum_vdw_vdb_corrected](images/adam_momentum_vdw_vdb_corrected.gif) <br> ![adam_rms_sdw_sdb_corrected](images/adam_rms_sdw_sdb_corrected.gif) <br>![adam_w_b](images/adam_w_b.gif)

* **Hyperparameters**

Hyperparameters | Choices
---|---
α|needs to be tune
β1|0.9 (dW)
β2|0.99 (dW<sup>2</sup>)
ε|10<sup>-8</sup>

#### Learning rate decay
* Formula decay

Formula | Remarks
---|---
![epoch decay](images/lr_decay_epoch.gif)|
![exponentially decay](images/lr_decay_exp.gif)|exponentially decay
![constant decay](images/lr_decay_k.gif)| k is a hyperparameter, t is the current iteration
learning rate decreases in discrete steps, descrease by one half after a while|


Note: 1 epoch = 1 pass through data
* Manual decay
