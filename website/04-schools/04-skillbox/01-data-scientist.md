---
layout: page
title: Skillbox, Профессия‌ ‌Data‌ ‌Scientist‌
description: Skillbox, Профессия‌ ‌Data‌ ‌Scientist‌
keywords: Skillbox, Профессия‌ ‌Data‌ ‌Scientist‌
permalink: /schools/skillbox/data-scientist/
---

# [Skillbox] Профессия‌ ‌Data‌ ‌Scientist‌

<br/>

Библиотека Keras, TF 1.4

<br/>

Смотрю "Профессия‌ ‌Data‌ ‌Scientist‌". Материал кажется норм.

Если я все правильно понял.
Чтобы следовать с начала по нарастающей, то следует начинать с блока по аналитеке.
Т.к. ML уже 2 блок.

<br/>

### Colab

Чтобы загрузить свой файл, можно добавить.

```
from google.colab import files
uploaded = files.upload()

import io
houses = pd.read_csv(io.BytesIO(uploaded['1.4_houses.csv']))
```

<br/>

Появится окно выбора файла. Выбрать файл со своего компьютера.

<br/>

### Модуль 01

<br/>

**Обучение с учителем**

- Регрессия [colab](https://colab.research.google.com/drive/1G1VKsb9FeoukcbrbmqPWFg1WtADnXjQc)
- Классификация [colab](https://colab.research.google.com/drive/19LJapwvlxAmEeDdyVV_7vm6XT1j7k8Dz)

<br/>

**Обучение без учителя**

- Кластеризация [colab](https://colab.research.google.com/drive/1mmsqUUZzB8zFJ0P0-nQZ03KtSQixuOTb)

<br/>

### Модуль 02: Жизненный цикл проектов ML

<br/>

### Модуль 03: Линейная регрессия

- [Урок 1. - 3.1 Постановка ML задачи линейной регрессии](https://colab.research.google.com/drive/1UrIkIl-QrzMPqAY-4G9rl8pMy-OpKwjt)

- [Урок 2. - 3.3 Продвинутый уровень понимания линейной регрессии](https://colab.research.google.com/drive/1FlLpVn217ag8xYOcar_ygOjixxeVPn8A)

- [Урок 5. - 3.5 Домашняя работа](https://colab.research.google.com/drive/1t6tT7t09I5I6nTV0zsMoshZrUSpNyX5w)

- [3.6 Метрики качества линейной регрессии](https://colab.research.google.com/drive/1YQr--K4dNzP5puuQqbFlmvJpsp0dAs9u)

* Mean Absolute Error (MAE) - сумма отклонений истинных значений y от предсказаний нашей модели. Потом мы эту сумму делим на количество точек - получаем среднюю ошибку. Метрика принимает только положительные значения! Чем ближе к нулю, тем лучше модель.
* Mean Squared Error (MSE) - Для каждого предсказанного значения y^ мы считаем квадрат отклонения от фактического значения и считаем среднее по полученным величинам. Метрика принимает только положительные значения! Чем ближе к нулю, тем лучше модель. (Если есть выбросы, лучше не применять)
* R2 (coefficient of determination) Наилучшее возможное значение 1.0, чем меньше тем хуже.

- [3.7 Домашняя работа](https://colab.research.google.com/drive/1m6MlFZLp08G4GQoDe0GxQ1DrqQwRNKra)

- [3.8 Трансформация входных данных для линейной регрессии](https://colab.research.google.com/drive/16PbgL5zxI_pFnHmtAkc-8YQaaTL79bSk)

Для борьбы с выбросами:

- Логарифмирование np.log
- Извлечение квадратного корня np.sqrt

Оба меняют абсолютные значения, но сохраняют порядок величин.

<br/>

- Standart Scaling (z-score normalization) - сглаживает данные, избавляет от выбросов.

- min-max normalization. Переносит все точки на отерзок [0-1]

* [3.9 Домашняя работа](https://colab.research.google.com/drive/10GCnc-xwG_4gcY800hnjw1qwH96P8kN9)

* [3.10 Полиномиальная регрессия](https://colab.research.google.com/drive/1Z63urCFPJ8xntW6kwX0Ui0-xbipD0Nm6)

* [3.11 Домашняя работа](https://colab.research.google.com/drive/1Z63urCFPJ8xntW6kwX0Ui0-xbipD0Nm6)

<br/>

### Модуль 04: Регуляризация

- [4.1 Регуляризация](https://colab.research.google.com/drive/1RXnrztNZiz3Fv-hTRtaQksAzIxm3qMFF)

Регуляризация - способ борьбы с переобучением.

1. Обучающую выборку разделяем на 2 части 80 / 20.

2. Выбираем метрику качества модели (для регрессии, например, RMSE)

3. Обучаем модель на тренировочном наборе данных

4. Делаем предсказания на валидационном наборе данных и вычисляем метрику качества

Признак переобучения:
Если качество на вилидации сильно хуже качества на обучающем сете.

- [4.2 Переобучение на примере линейной регрессии](https://colab.research.google.com/drive/1WuGpuX-lr63Kdqk1f50lYafJrE5mOAni)

- [4.3 Домашняя работа](https://colab.research.google.com/drive/14yZ-lxyV7k-qLBATqNfD4jZYETq0LJjT)

<br/>

**Регуляризация в sklearn:**

- Ridge
- Lasso

Оба принимают на вход параметр регуляризации alpha, который принимает значения от 0 до 1. Чем ближе к единице, тем регуляризация сильнее.

<br/>

L2 регуляризация (также называют гребневой регрессией) - в целевую функцию добавляются квадраты коэффициентов регрессии. Если фичей мало, использовать ее.

L1 регуляризация (в sklearn.linear_model.Lasso) - добавляются модули весов. Если фичей много - сотни или тысячи рекомендуют использовать ее. Т.к. она обнулит фичи, которые значимыми не являются.

<br/>

- [4.4 Математическая магия регуляризации](https://colab.research.google.com/drive/1rEvBBGUjXfdkdyobuB_vbej7DR0ZmlRH)

<br/>

Выбрать правильное значение коэффициента регуляризации поможет процедура, которая называется "отложеннй контроль".

В цикле выбираем разные варианты и выбираем тот который лучше.

<br/>

- [4.7 Обучение моделей с помощью градиентного спуска](https://colab.research.google.com/drive/1TbdgmyPYp0I-dl1ov2i6VeNe6RfZMAgU)

<br/>

- [4.8 Домашняя работа](https://colab.research.google.com/drive/1W8_bzO22H62Pc_AJ-wQYmi6YftryNRZS)

<br/>

- [4.9 Математическая магия градиентного спуска](https://colab.research.google.com/drive/1nrnUE_5s6EsIkt1-R596BeUlSKv_zjQL)

<br/>

- [4.12 Домашняя работа](https://colab.research.google.com/drive/177ot4WfIDLxmw0_On-7nh0BUQn09OxTl)

<br/>

### Модуль 05: Алгоритм KNN

- [5.1 Алгоритм KNN](https://colab.research.google.com/drive/1KunpzfHJqAnf7ThPZcprdRrYi7qRSG5k)

- [5.3 Урок 3. kNN + Домашняя работа](https://colab.research.google.com/drive/1QLmBqeQtfnNVn3TRAyRRcr8AP1VpDd3M)

- [5.4 Наивный баесовский классификатор](https://colab.research.google.com/drive/1wb9hPIbvWIsmo1ppFKpTGGOSreKhrpzs)

- [5.6 Домашняя работа](https://colab.research.google.com/drive/19iYAd9AdsmyPblQqpEtHrJnGcDXW9ZKY)

- [5.7 Алгоритм Decision Trees](https://colab.research.google.com/drive/1A7rMtcZCxY7XEuVVKIbpSRz29K-s7wAT)

- [5.7 Алгоритм Decision Trees](https://colab.research.google.com/drive/1A7rMtcZCxY7XEuVVKIbpSRz29K-s7wAT)

- [5.8 Домашняя работа](https://colab.research.google.com/drive/1ZUsgpCKISxgFl_kIzoeiWh5S-c88QC9l)

<br/>

### Модуль 06: Метрики качества классификации

С помощью Confusion Matrix (Матрица ошибок)

- Accuracy (Доля правильных ответов)
- Precision (Точность)
- Recall (Полнота)

- [6.1 Метрики качества классификации](https://colab.research.google.com/drive/1rdcNihCXzhfGhECVte4wqsY3fdsKMtCi)

- [6.2 Домашняя работа](https://colab.research.google.com/drive/1ktR3rAEVo-2LoQuw5UaxGctayn4-oC0K)

- [6.3 Метрики качества классификации. Часть 2](https://colab.research.google.com/drive/12RDSNQ9saRmbJ486NIxlNROFJWkp9iYx)

* F-мера
* Area Under Curve - Receiver Operating Characteristic Curve (AUC-ROC)
* Logloss (Логистическая функция потерь)

- [6.4 Домашняя работа](https://colab.research.google.com/drive/1bDmI0PzuxyDUyA4oh5ug1ITQ5lyhwGAG)

- [6.5 Мультиклассовая классификация](https://colab.research.google.com/drive/1YkyFFw0xgzL7y8DQ1eeZQLLk6dCVT0B5)

* OvA (One-versus-all) Один против всех

- [6.6 Домашняя работа](https://colab.research.google.com/drive/1ongqGhcpZMP_kHTIC_2pqfXLSFl6PRN3)
