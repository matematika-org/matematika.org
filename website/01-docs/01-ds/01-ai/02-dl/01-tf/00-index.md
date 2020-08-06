---
layout: page
title: TensorFlow (Deep Learning)
description: TensorFlow (Deep Learning)
keywords: TensorFlow, Deep Learning
permalink: /ds/ai/dl/tf/
---

# TensorFlow (Deep Learning)

![Tensor](/img/docs/ds/ai/dl/tensor.png 'Tensor'){: .center-image }

<br/>

С версии 1.6 tf использует AVX инструкции. Поддерживает ваш проц такие или нет можно посмотреть в ubuntu здесь:

    $ cat /proc/cpuinfo

Чтобы использовать tf на проце, который не поддерживает AVX инструкции, нужно использовать версию 1.5.

<br/>

## Подготовка окружения

<br/>

### [Лучше запустить в виртуальном окружении](/ds/ai/devtools/python/virtualenv/)

<br/>

### [Запуск контейнера с TensorFlow в docker](/ds/ai/devtools/python/docker/)

<br/>

**Узнать версию python3**

    from platform import python_version
    print(python_version())

**Узнать версию установленной библиотеки tensorflow**

    import tensorflow as tf
    print(tf.__version__)

<br/>

### Примеры:

https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/quests/scientific/coastline.ipynb

<br/>

Пример предсказания цены на дом

https://github.com/vijaykyr/tensorflow_teaching_examples/blob/master/housing_prices/cloud-ml-housing-prices.ipynb

Predicting Baby Weight with TensorFlow on Cloud ML Engine (GSP013)

https://github.com/GoogleCloudPlatform/training-data-analyst/blogs/babyweight/train_deploy.ipynb

<br/>

### [Convolutional Neural Networks - MNIST - распознавание цифр](/ds/ai/dl/tf/mnist/)
