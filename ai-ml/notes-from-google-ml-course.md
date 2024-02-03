---
description: Course taken in Nov 2018.
---

# Course Notes - Google ML Intro

### Course Details

Title: **Introduction to Machine Learning**

Link: [https://developers.google.com/machine-learning/crash-course/ml-intro](https://developers.google.com/machine-learning/crash-course/ml-intro)

### Introduction

Peter Norvig, Director of Research at Google gives the intro explaining how ML helps software engineers - reduce the time programming, customize products for specific people, complete seemingly impossible tasks. Also, philosophical reason - it changes the way you think about a problem. Focus shifts from mathematical science to a natural science, running experiments, use statistics instead of logic to analyze the results.

### Tools

Collaboratory - Free Jupiter notebook environment that runs fully in the cloud. [https://colab.research.google.com/notebooks/welcome.ipynb](https://colab.research.google.com/notebooks/welcome.ipynb)

Pandas - Python library for data structures and data analysis. It uses **DataFrames** and **Series**. It can load an entire file into a DataFrame, show interesting statistics about data, plot a histogram etc., More info at [https://colab.research.google.com/notebooks/mlcc/intro\_to\_pandas.ipynb](https://colab.research.google.com/notebooks/mlcc/intro\_to\_pandas.ipynb). You can run code in this environment and see the results in real-time.

### Framing

**Supervised ML** - System that combines inputs to provide useful predictions on data that was never seen before.

* **Label** - target that we are predicting; eg: "spam", "not spam". It is the **y** variable in linear regression.
* **Feature** - input variable that describes the data (eg: words in the email, to/cc fields, email headers). It is the **x** variable in simple linear regression.
* **Example** - A particular instance of data. It can be **labeled** (includes the feature/s and the label) or **unlabeled** (contains feature, but no label). We train the models using labeled examples and then use that model to predict the label of unlabeled examples.
* **Model** - defines the relationship between features and labels. eg: spam detection model may identify some features as strongly associated with spam. Models have two phased - Training (creating/learning the model) and Inference (apply the trained model to unlabeled examples).
* Types of models
  * Regression model: predicts continuous value (price of house in CA)
  * Classification model: predicts discrete values (is the email spam? is this an image of dog/cat/lion)

### Descending into ML

* Linear Regression - method of finding a straight line or hyperplane that fits a set of points in the best way.   **y = wx + b** (w is the weight and b is the bias)
* Loss - penalty of bad prediction. Number that indicates how bad the prediction was on a single example.&#x20;
* Goal of training a model is to find a set of weights and biases that have _low_ loss _on average_ across all examples.
* One of the methods to represent Loss is:
  * **L2 Loss (**aka **Squared Loss):** the square of the difference b/w predicted value and observed value of label. MSE = Mean Squared Error; D = data set that contains N pairs of examples (x, y)

$$
MSE = \frac{1}{N}\sum_{(x,y) \epsilon D} (y - prediction(x))^2
$$
