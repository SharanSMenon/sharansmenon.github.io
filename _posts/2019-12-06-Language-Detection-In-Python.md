---
title: Language Detection in Python
published: true
---

In this tutorial, you will learn how to use a model that can predict around 11 different languages. Sometimes, instead of building a model and training it, etc., you just want a model that is accurate and easy to use. This is the aim of the tutorial, just like the previous one where I talked about sentiment analysis.

This model is also trained in scikit-learn and you can learn more about this model by checking out the repository:

[https://github.com/SharanSMenon/ml-models/tree/master/language_detection/sklearn](https://github.com/SharanSMenon/ml-models/tree/master/language_detection/sklearn)

The languages include

1. English
2. Spanish
3. French
4. Italian
5. German
6. Dutch
7. Japanese
8. Portuguese
9. Arabic
10. Russian
11. Polish



## How to use it

Below is to code to access the model. You have to pass in a string to the `predict` function as shown below.

> **Note**: Make sure that you have scikit-learn installed. 

```python
import pickle
from urllib.request import Request, urlopen
modelreq = Request("https://raw.githubusercontent.com/SharanSMenon/ml-models/master/language_detection/sklearn/language_detection.p")
m = urlopen(modelreq)
langs_dict = { 'ar': "Arabic", 'es': 'Spanish', 'en': 'English',
    'fr': 'French', 'de': 'German', 'it': 'Italian',
    'ja': 'Japanese', 'nl': 'Dutch', 'pl': 'Polish',
    'pt': 'Portugese', 'ru': 'Russian'
}
langs = ['ar', 'de', 'en', 'es', 'fr', 'it', 'ja', 'nl', 'pl', 'pt', 'ru']
model = pickle.load(m)
def predict(sent):
    predicted = model.predict([sent])
    lang = langs[predicted[0]]
    lg = langs_dict[lang]
    return lg
print(predict("This is english")) # English
print(predict("Hola, como estas")) # Spanish
print(predict("Dies ist ein Test, um die Sprache zu erkennen.")) # German
print(predict("Ceci est un test de d\xe9tection de la langue.")) # French
```

If the script ran successfully, you should see the following:
```
English
Spanish
German
French
```

You can see that the model predicted the languages correctly. This is what we will be building today. The model that you saw above has around 95% accuracy.

So there you have it, an accurate model that can detect languages. 
