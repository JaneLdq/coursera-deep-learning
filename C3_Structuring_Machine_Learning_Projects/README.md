# Course 3 - Structuring Machine Learning Projects

## Evaluation Metric
#### Single number evaluation metrics
Metric | Definition
--- | ---
Precision | True Positive / (True Positive + False Positive)
Recall | True Positve / (True Positive + False Negative)
F1 Score | 2 * Precision * Recall / (Percision + Recall)

#### Satisficing and Optimizing Metrics
Type | Definition
--- | ---
Optimizing Metric | the metric you want to maximize
Satisficing Metric | it has just to be good enough

:chestnut: **Example**

Classifier | Accuracy | Running time | -
--- | --- | --- | ---
A | 90% | 80ms |
B | 92% | 95ms | √
C | 95% | 1500ms |

Cost = accuracy - 0.5 * runningTime

Suppose You want to maximize accuracy and subject to running time <= 100ms, so the Accuracy is the optimizing metric and runnint time is the satisficing metric here.


## Train/Dev/Test Distribution
* Choose a dev set and test set to reflect data you expect to get in the future and consider important to do well on.
* Ensure your dev set and test set from the **SAME** distribution.

**Note: When to change dev/test set distribution or your evalution metrics?**

When your evaluation metric is no longer correctly rank ordering preferences between algorithms, that's a sign that you should change your evalution metric or perhaps your dev set or test set.


## Human-level Perfomance
### Why compare to human-level performance?

So long as ML is worse than humans, you can:
* Get labeled data from humans
* Gain insight from manual error analysis: why didi a person get this right?
* Better analysis of bias/variance

### What is Avoidable Bias?
**Bayse Optimal Error**: the perfomance approaches but never surpasses this theoretical limits

**Using Human-level error as a proxy for Bayes error.**

:chestnut: **Example**

Error | #1 | #2
--- | --- | ---
Humans (≈ Bayes)| 1% | 7.5%
Training Set | 8% | 8%
Dev Set | 10% | 10%
**-**| Focus on **bias** (between humans/train) | Focus on **variance** (between train/dev) 

* **Avoidable bias** - the difference between humans error and training set error
* **Variance problem** - the difference between training set error and dev set error

### How to Reducing Bias & Variance?

Error | Tactics
---|---
Avoidable Bias | Train bigger model <br>Train longer/better optimization algorithms <br>NN architecture/hyperparameters search
Variance Problem | More data <br>Regularization