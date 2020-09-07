---
layout: page
title: Deep Learning (Глубокое обучение) Нейронные сети
description: Deep Learning (Глубокое обучение) Нейронные сети
keywords: Deep Learning, Глубокое обучение, Нейронные сети
permalink: /ds/dl/
---

# Deep Learning (Глубокое обучение) Нейронные сети

Я пытаюсь разобраться. Добавляйте, кому есть что добавить. Исправляйте, где я заблуждаюсь.

<br/>

### Лучшее из коротких объяснение как работают нейронные сети

<div align="center">

    <iframe width="853" height="480" src="https://www.youtube.com/embed/8IrD9jfuVQM?start=163" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

<br/>

**Классификация нейронных сетей:**

- Dense Networks
- Convolutional Networks (ConvNets) - (MNIST - распознавание цифр)
- Recurrent Neural Networks (RNNs) - (распознавание речи)
- Reinforecement Learning
- Generative Adversarial Networks (GANs)

<br/>

![Deep Learning](/img/docs/ds/dl/dl-01.png 'Deep Learning'){: .center-image }

<br/>

![Deep Learning](/img/docs/ds/dl/dl-02.png 'Deep Learning'){: .center-image }

<br/>

![Deep Learning](/img/docs/ds/dl/dl-03.png 'Deep Learning'){: .center-image }

<br/>

![Deep Learning](/img/docs/ds/dl/dl-04.png 'Deep Learning'){: .center-image }

<br/>

![Deep Learning](/img/docs/ds/dl/dl-05.png 'Deep Learning'){: .center-image }

<br/>

![Deep Learning](/img/docs/ds/dl/dl-06.png 'Deep Learning'){: .center-image }

<br/>

![Deep Learning](/img/docs/ds/dl/dl-07.png 'Deep Learning'){: .center-image }

<br/>

## Библиотеки грубокого обучения

<br/>

### [TensorFlow](/ds/dl/tf/)

TensorFlow - библиотека от Google для ML/DL. Можно запускать обычным способом, в docker контейнерах, в том числе в kubernetes кластерах (инструмент для запуска кучи контейнеров на куче серверов). Есть специальный проект kubeflow, для работы tensorflow в kubernetes. Скрипты для развертывания локального kubernetes кластера в linux у меня есть. Спросить в чате, если нужно.

TensorFlow, вроде как, был сложен для программистов и была написана библиотека упрощающая работу с ним - keras. Библиотека набрала популярность и в Google решили добавить наработки из этой библиотеки во вторую версию TensorFlow, которая пока beta. В общем, если выбирать библиотеку для изучения DL, наверное лучше сразу начинать копаться со второй версии TensorFlow.

<br/>

### [Keras](/ds/dl/keras/)

Работает над TensorFlow или дургой библиотекой Theano.

<br/>

### PyTorch

Вроде как, "более гибкая" библиотека, чем keras. Так сказал автор курса от Отус по ML.

<br/>

### Lasagna (построена на основе библиотеки theano)

Хз, что за библиотека такая

<br/>

**Функции активации:**

- Блок линейной ректификации - Rectified Linear Unit (ReLU)
- ELU
- Сигмоида (softmax)
- Гиперболический тангенс
- Линейная функция
- Логистическая фукнкция

<br/><br/>

По функциям активации в tensorflow1 почитать [Орельен Жерон] Прикладное машинное обучение с помощью Scikit-Learn и TensorFlow [RUS, 2018]

Полный перечень функций активации keras приведен на странице: keras.io/activations/

<br/>

## Обучающие материалы:

### [Книги по Deep Learning](/books/ds/dl/)

### [Видеокурсы по Deep Learning](/videos/ds/dl/)

<br/>

### Practical Deep Learning for Coders

https://github.com/fastai/courses
