---
title: Sentiment analysis in python
published: true
---

Hello and in this tutorial, we will learn how to do sentiment analysis in python. We will make a script that loads in a ready-made model and we will use it to predict the sentiment of text

## What is the ready-made model?

I have a repo on my GitHub that is called `ml-models`. This repo, as its name suggests, contains a lot of machine learning models. I am constantly adding new models and improving existing ones, but the repo contains a sentiment analysis model. This is the model that we will be used for sentiment analysis. So, go check the repo out at this URL: 

[https://github.com/SharanSMenon/ml-models](https://github.com/SharanSMenon/ml-models)

## Making the script

I will explain this code step by step, so follow along.

Ok. Let's make the script now that we know about the model. Open any python file in your favorite editor and add the following code:

```py
import pickle
from urllib.request import Request, urlopen
```

We are importing two libraries that will help us to access the model. The model is stored on the internet so we need `urlopen` instead of the normal `open` function. We will then unpickle the model so that we can use it. 

Add the following bit of code to your script:

```py
modelreq = Request("https://raw.githubusercontent.com/SharanSMenon/ml-models/master/sentiment_analysis/scikit-learn/sentiment_model.p") # Getting the model
vectorreq = Request("https://raw.githubusercontent.com/SharanSMenon/ml-models/master/sentiment_analysis/scikit-learn/vectorizer.p") # Getting the vectorizer
```

This is where the model is hosted, so we need to get it from there.

Add the following piece of code to your script:

```py
m = urlopen(modelreq)
v = urlopen(vectorreq)

model = pickle.load(m) # The model
vectorizer = pickle.load(v) # The vectorizer
```

The vectorizer is to process the string before we feed it to the model. We load the model and the vectorizer using `pickle.load`. 

We will add a helper function for predicting the sentiment of some text:

```python
def predict(s):
    transformed = vectorizer.transform([s]).toarray()
    pred = model.predict(transformed)
    return pred[0]
```

This processes the string before feeding it to the model. The model requires an array of strings so we return the 0th element.

```py
print(predict("This sucks")) # returns "neg"
print(predict("This is great")) # returns "pos"
```

This is the last piece of the code and the script is complete. You can run the script and you should get the following in your output:

```
neg
pos
```

If you get this, that means the code ran successfully. Here is the full script:

```py
import pickle
from urllib.request import Request, urlopen
modelreq = Request("https://raw.githubusercontent.com/SharanSMenon/ml-models/master/sentiment_analysis/scikit-learn/sentiment_model.p") # Getting the model
vectorreq = Request("https://raw.githubusercontent.com/SharanSMenon/ml-models/master/sentiment_analysis/scikit-learn/vectorizer.p") # Getting the vectorizer
m = urlopen(modelreq)
v = urlopen(vectorreq)
model = pickle.load(m)
vectorizer = pickle.load(v)
def predict(s):
    transformed = vectorizer.transform([s]).toarray()
    pred = model.predict(transformed)
    return pred[0]
print(predict("This sucks")) # returns "neg"
print(predict("This is great")) # returns "pos"
```

The script is just under 20 lines and it can do sentiment analysis. This is really powerful and you can do a lot.

## Conclusion

Well folks, that's it for this tutorial and I hope to see you some other time. Have fun with your newfound capabilities and bye for now!
