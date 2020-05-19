---
title: "Random Forests in Python"
published: true
---

In this tutorial, you will learn how to implement random forests with scikit learn. Both Random forests can be used for classification and regression. We will use it today for classification. Let's get started!

## Getting the data

Download the data from this [link](https://www.kaggle.com/ronitf/heart-disease-uci). This is heart disease data. We will be predicting whether a patient has heart disease or not based on some inputs. This is a really famous dataset.

## Getting started and importing libraries

Let's import all the libraries that we need to make a Decision Tree and a Random Forest. We will be using `scikit-learn` for our models. We will also use scikit learn to generate our data.

### Installing scikit-learn

```sh
pip install scikit-learn
```

> Make sure that you have pandas and numpy installed. You can also install matplotlib for data visualization.

Let's code now! We will start by importing all libraries needed:

```python
import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
```

Let's load in the data with pandas
```python
df = pd.read_csv("heart.csv")
df.head()
```

|age|sex|cp|trestbps|chol|fbs|restecg|thalach|exang|oldpeak|slope|ca|thal|target
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|63|1|3|145|233|1|0|150|0|2.3|0| 0|1|1|
|37|1|2|130|250|0|1|187|0|3.5|0|0|2|1|
|41|0|1|130|204|0|0|172 |0|1.4|2|0|2|1|
|56|1|1|120|236|0|1|178|0|0.8|2|0|2|1|
|57|0|0|120|354|0|1|163|1|0.6|2|0|2|1|

We will now seperate the data from the target

```python
X = df.drop("target", axis=1) # This is our data
y = df['target'] # These are our targets
```

Now, we will split the data into a training and testing set.

```python
# Importing a helper function from scikit-learn
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25)
```

We now have 4 sets. `X_train`, `X_test`, `y_train`, `y-test`. We will train the model with `X_train` and `y-train` and we will give `X_test` as the test data for the model. We will see its performance with `y-test`. Let's continue.

```python
print(X_train.shape)
print(X_test.shape)
```

    (Out)
    (227, 13)
    (76, 13)

Let's now build and train the Random Forest classifier

```python
from sklearn.ensemble import RandomForestClassifier
```

```python
rfc = RandomForestClassifier(n_estimators=250)
# Tweak n_estimators. I chose 250
```

We have built the model with 250 trees, let's train the model

```python
rfc.fit(X_train, y_train)  # Just one line needed
```

As you can see, we only needed 1 line to train the model. We will now evaulate the model. In the following cell, we will feed the test data to the model.

```python
preds = rfc.predict(X_test)
```

We will now see how well the model did on the test data. But first, we will import more functions from scikit learn.

```python
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
```

We will do the following things:

1. We will see the accuracy of the model
2. We will print a classification report using the `classification_report` function that `scikit-learn` provides
3. We will print a confusion matrix.

Let's go!

```python
print(accuracy_score(y_test, preds))
```

    (Out)
    0.7763157894736842

We get an accuracy of 78%. That's all right for the model. Using advanced technique, we can bring this accuracy to 80% or even 90%. Let's print the confusion matrix and the classification report.

```python
print(classification_report(y_test, preds))
```
    (Out)
               precision    recall  f1-score   support

           0        0.69      0.80      0.74        30
           1        0.85      0.76      0.80        46

    accuracy                            0.78        76
    macro avg       0.77      0.78      0.77        76
    weighted avg    0.79      0.78      0.78        76


Finally, we will print the confusion matrix.

```python
print(confusion_matrix(y_test, preds))
```

    (Out)
    array([[24,  6],
           [11, 35]])

All right. You can see that this model does pretty well on the test set.

## Conclusion

We have built a Random Forest Classifier that can classify whether a patient has heart disease or not. The model has good performance but it can be improved. Some problems that we had was that we used a pretty basic approach and that we didn't have too much data. Advanced techniques and more data can lead to higher accuracies.

It is really easy to build and train a Random Forest Classifier with Scikit-learn.