---
layout: page
title: Орельен Жерон - Прикладное машинное обучение с помощью Scikit-Learn и TensorFlow [RUS, 2018]
description: Орельен Жерон - Прикладное машинное обучение с помощью Scikit-Learn и TensorFlow [RUS, 2018]
keywords: Орельен Жерон, Прикладное машинное обучение с помощью Scikit-Learn и TensorFlow
permalink: /books/ds/ml/ru/hands-on-machine-learning-with-scikit-learn-and-tensorflow/
---

# [Орельен Жерон] Прикладное машинное обучение с помощью Scikit-Learn и TensorFlow [RUS, 2018]

Запланировано на сентябрь 2-е издание. Если кто найдет и кому не жалко, поделитесь.

На сайте складчик, скидываются по 90 руб. А меня там забанили.

<br/>

https://github.com/ageron/handson-ml

<br/>

**В ubuntu:**

Подготовил окружение как <a href="/ds/ai/devtools/python/virtualenv/">здесь</a>

<br/>

**Импортируем данные**

// Инфа
https://github.com/ageron/handson-ml/blob/master/02_end_to_end_machine_learning_project.ipynb

<br/>

```python
import os
import tarfile
from six.moves import urllib

DOWNLOAD_ROOT = "https://raw.githubusercontent.com/ageron/handson-ml/master/"
HOUSING_PATH = os.path.join("datasets", "housing")
HOUSING_URL = DOWNLOAD_ROOT + "datasets/housing/housing.tgz"

def fetch_housing_data(housing_url=HOUSING_URL, housing_path=HOUSING_PATH):
    os.makedirs(housing_path, exist_ok=True)
    tgz_path = os.path.join(housing_path, "housing.tgz")
    urllib.request.urlretrieve(housing_url, tgz_path)
    housing_tgz = tarfile.open(tgz_path)
    housing_tgz.extractall(path=housing_path)
    housing_tgz.close()
```

```
fetch_housing_data()
```

```python
import pandas as pd

def load_housing_data(housing_path=HOUSING_PATH):
    csv_path = os.path.join(housing_path, "housing.csv")
    return pd.read_csv(csv_path)
```

```python
housing = load_housing_data()
housing.head()
```
