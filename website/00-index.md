---
layout: page
title: Математика
permalink: /
---

# Математика

<br/>

### Допустим вы за каким-то хреном решили изучать DataScience, BigData, BlockChain, IoT, математику, статистику, теорию вероятности и т.д.

Большинство людей всеравно копают приблизительно тоже самое и изучают те же самые материалы по тем же самым источникам. Если копаете, что-то более менее интересное или что нужно записать, оставляйте ссылки на то куда вы это записываете (гитхаб, блог, ворд документ) или пишите прямо сюда.

<br/>

![Simple linear regression model](/img/simple-linear-regression-model.png 'Simple linear regression model'){: .center-image }

<br/>

### [Stepic] Нейронные сети и компьютерное зрение [RUS, 2020]

https://stepik.org/course/50352/promo

https://github.com/RomanovMikeV/deep-learning-lectures/

https://github.com/SlinkoIgor/Neural_Networks_and_CV

<br/>

### [YouTube] Математика на QWERTY

Все экзамены прошли и теперь можно со спокойной душой узнать, зачем же были нужны эти <a href="https://www.youtube.com/watch?v=ZZMCDNAmcs4">производные</a>, <a href="https://www.youtube.com/watch?v=JzT0-0bBY9M">интегралы</a>,<a href="https://www.youtube.com/watch?v=telTRUTzHd4">логарифмы</a>, <a href="https://www.youtube.com/watch?v=xsLbbP-6_r8">пределы</a>, <a href="https://www.youtube.com/watch?v=2QQrAbHreLY">тригонометрия</a>.

<br/>

### [YouTube] куча материалов на русском из топовых ВУЗов.

https://www.youtube.com/channel/UCeDm7xMiUD2cDLwek8sIevA/playlists

Надо, чтобы кто-то выкачал по нашей теме и разложил по полочкам.

Затянули со скачиванием. Ролики закрыты.
Если кто может скачать, поделитесь.
Или когда откроют, дайте знать, чтобы мы скачали.

**UPD. Есть предположение, что материалы доступны на сайте openedu.**

https://openedu.ru/course/msu/CALC1/

<!--

<br/>

### Возможно поду собеседоваться на позицию аналитика Data Science

Что посоветуете почитать / посмотреть по следующему?

- Знания статистики (аппроксимация распределений, временные ряды, статистические критерии);
- Знания методов Data Mining (кластеризация, регрессии, SVM, дерево решений и др.).

По второй части, все вроде бы знакомое.
По хорошему, следовало бы разобрать и добавить на сайт информацию по всему этому.

-->

<br/>

### [Derek Banas] Learn Algebra

https://www.youtube.com/watch?v=B_WCI_A944E

<br/>

### Hyperledger - корпоративная платформа на BlockChain

Возникли сложности и с изучением и с запуском примеров. Читаю книгу [Nakul Shah] Blockchain for Business with Hyperledger Fabric: A complete guide to enterprise Blockchain implementation using Hyperledger Fabric [ENG, 2019]

Если кому интересно и тоже хочет поразбираться или подсказать что не так, какие-то наработки <a href="/books/blockchain/hyperledger/en/fabric/blockchain-for-business-with-hyperledger-fabric/">здесь</a>

<br/>

### [Derek Banas] Statistics Tutorial

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/videoseries?list=PLGLfVvz_LVvQjNJr85J4U_lxDg8vgqvcO" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

### [foo52ru] Расскажет про свои познания в копании нейронных сетей

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/videoseries?list=PLnmlxA5EUR3E15AtCyigwbsurUFHG6MNN" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

### [Орельен Жерон] Прикладное машинное обучение с помощью Scikit-Learn и TensorFlow [RUS, 2018]

Приглашаю к коллективному чтению и при необходимости, к обсуждению.

<a href="/books/ds/ml/ru/hands-on-machine-learning-with-scikit-learn-and-tensorflow/">Наработки</a>

<br/>

### [Jesse E. Agbe] Building Machine Learning Web Apps with Python [ENG, 2020]

https://www.udemy.com/course/building-machine-learning-web-apps-with-python/

Там индусятина какая-то, но зато какой-никакой а проект

<br/>

### [Sudhir G] Face Recognition Web App with Machine Learning in FLASK [ENG, 2020]

https://www.udemy.com/course/build-face-recognition-app-using-machine-learning-in-flask/

Там индусятина какая-то, но зато какой-никакой а проект

<!--

<br/>

pip install -r requirements.txt

```
numpy
scipy
matplotlib
pandas
jupyter
sklearn
```

    $ pip install opencv-python

-->

<br/>

### [Dr. Jon Krohn] Deep Learning with TensorFlow: Applications of Deep Neural Networks to Machine Learning Tasks [ENG, 2017]

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/wBgW3ZtlPT8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

https://www.oreilly.com/library/view/deep-learning-with/9780134770826/

https://github.com/the-deep-learners/TensorFlow-LiveLessons

<!--

В ubuntu:

```
$ mkdir -p ~/projects/dev/dl
$ cd ~/projects/dev/dl
$ git clone https://github.com/matematika-org/TensorFlow-LiveLessons
$ cd TensorFlow-LiveLessons/

$ sudo apt-get update && sudo apt-get upgrade
$ sudo apt-get install -y python3.6
$ sudo apt-get install -y python3-pip

$ python3 --version
Python 3.6.9

$ sudo apt-get install -y virtualenv
$ virtualenv --system-site-packages -p python3 tf_1
$ source tf_1/bin/activate

$ pip install --upgrade pip

$ {
    pip install --upgrade tensorflow==1.0
    pip install --upgrade tflearn==0.3.2
    pip install --upgrade keras==2.0.8
    pip install --upgrade nltk==3.2.4
    pip install --upgrade gensim==2.3.0
    pip install --upgrade gym==0.9.4
    pip install --upgrade jupyterlab
}

<br/>

    $ jupyter notebook --ip 0.0.0.0 --port 8888

```
<br/>

```
import tensorflow
import tflearn
import keras
import nltk
import gensim
import gym

print(tensorflow.__version__)
print(tflearn.__version__)
print(keras.__version__)
print(nltk.__version__)
print(gensim.__version__)
print(gym.__version__)

Пока не все работает.

```
-->

<br/>

### Mathematics for Machine Learning

"We wrote a book on Mathematics for Machine Learning that motivates people to learn mathematical concepts. The book is not intended to cover advanced machine learning techniques because there are already plenty of books doing this. Instead, we aim to provide the necessary mathematical skills to read those other books."

https://mml-book.com/

https://www.coursera.org/specializations/mathematics-machine-learning

<br/>

### ODSC East 2019 (Open Data Science Conference)

https://www.oreilly.com/library/view/odsc-east-2019/9780136746874/

<br/>

### [QwikLabs] Лабораторки по ML/DL, BigData, DataScience в облаках Google и Amazon

**UPD. Месяц бесплатно из за вируса**

Подробности здесь:

https://go.qwiklabs.com/qwiklabs-free

<br/>

Есть сайт для обучению облачным технологиям qwiklabs.com. Предоставляют доступ к облачным решениям от AWS и Google + примеры как со всем этим работать. В том числе примеры по ML, BigData, DataScience.

Решение платное, но можно поискать купоны / промо и т.д. Я например, нашел себе здесь аккаунт на месяц.

https://medium.com/@sathishvj/qwiklabs-free-codes-gcp-and-aws-e40f3855ffdb

Просто залогинился по ссылке.

Если обнаружится еще какая халява, дайте знать в телеграмме.

Если будете разбирать, можете добавить информацию на этот сайт. Или просто для себя потыкать в облака палкой.

Предлагаю начать <a href="/clouds/google/qwiklabs/baseline-data-ml-ai/">вот с этого</a>.

Или этого:  
https://www.qwiklabs.com/quests/5

Впрочем, если опыта работы с облаками у вас совсем нет (лично у меня, когда я только приступил, его почти не было), наверное следует начать вообще вот с этого:
https://www.qwiklabs.com/quests/23

<br/>

![qwikLabs-monthly-subscription](/img/qwikLabs-monthly-subscription.png 'qwikLabs-monthly-subscription'){: .center-image }

<br/>
<br/>

![Сбертех новые технологии](/img/humor/sber.jpg 'Сбертех новые технологии'){: .center-image }

<br/>

![Греф Сбербанк потерял миллиарды из-за ошибок ИИ](/img/humor/gref.jpg 'Греф Сбербанк потерял миллиарды из-за ошибок ИИ'){: .center-image }

<br/>

### Программисты не нужны и мы с ними боремся

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/3VRddnuTR9M" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

### Приглашаю присоединиться к изучению следующих курсов

- Spark and Python for Big Data with PySpark
- Scala and Spark for Big Data and Machine Learning

Другие материалы автора:  
https://docs.google.com/document/d/1TfB48iJcCAPaQYiOgB70_QgBXyGaU33nYyUZ6lgtLl8/edit

- Build streaming applications using Apache Kafka and Scala (Индус с акцентом)

* Качнул книги:

- John T., Misra P. - Data Lake for Enterprises [2017, ENG]
- Practical Data Science: A Guide to Building the Technology Stack for Turning Data Lakes into Business Assets

<!--

<br/>

### Времени на раскачку как известно нет

- Machine Learning (ML) - скучно
- Deep Learning (DL) - скучно
- Reinforcemetn Learning (RL) - интересно, но сложно. Мой уровень прокачки персонажа пока не позволяет использовать эти навыки.

<br/>

**Основные библиотеки:**

- scikit learn (python)
- pytorch (Facebook) (python)
- tensorflow (Google) (python)
- keras (вроде как теряет актуальность после выхода tensorflow 2.0) (python)
- mahout (apache) (hadoop)
- spark ml (apache) (pyspark / scala)

В части machine learning делают приблизительно тоже самое.

<br/>

**Доп библиотеки без которых никуда:**

- numpy
- pandas

Остальное менее интересно.

Если есть знания и программы, делитесь если не жалко времени.

-->

<br/>

### Куча материалов по математике

**В том числе:**

- Линейная алгебра
- Матан
- Математическая логика
- Статистика
- Дискретная математика
- Дифуры

https://cloud.mail.ru/public/499B/4XtQvr5tF

<!--

<br/>

### Приглашаю коллективно почитать и разобрать примеры из книги Том Уайт› Hadoop: Подробное руководство [RUS, 2013]

По 50 страничек в будний день.


![Hadoop Подробное руководство](/img/books/bigdata/ru/Hadoop-The-Definitive-Guide-rus.jpg "Hadoop Подробное руководство"){: .center-image }

Книгу найдете сами.

<a href="/ds/bigdata/hadoop/">Отправная точка</a>

-->

<br/>

### Товарищи студенты и поступающие в высшие ученые заведения !!!

Если будет желание поделиться чем-то полезным дайте знать. Можете сами добавлять сюда информацию по изучаемым дисциплинам. При желании можно оставлять ссылки на свои профили в facebook, linkedin.

<br/>

### Сразу должен извиниться !!!

Я мало что помню из того, что изучал в университете (хотя и учился хорошо). В последнее время занимался задачами связанными с программированием, но без применения чего-либо похожего на задачи связанные с математикой, статистикой, теорией вероятности и т.д. т.е. типичный быдлокодинг, формошлепство и т.д.

Поэтому, если вы здесь хотите найти какие-либо полезные знания для себя, у вас это не получится. (Надеюсь, что пока) Можете не тратить свое время.

Я планирую ковырять ML и BigData, если хотите со мной, добавляйтесь в телеграм чат.

<br/>

Также вот что было <a href="/videos/">найдено</a>. Может кому-нибудь тоже будет интересно и он себе накачает самостоятельно.

Если вы изучаете математику и готовы делиться своими знаниями, можете добавлять их сюда. Как это сделать можно обсудить в телеграм чате.

И да, мы не будем тут выкладывать материалы запрещенные авторским правом. Но обсуждать, может и будем.

<br/>

### Хакеры D1G1R3V взломали почту сотрудников из МГУ и 0day technologies

Злодеи хотят нас контроллировать, следить, анализировать, блокировать нам ресурсы, присваивать метки для негласной слежки.

Нас интересуют в большей степени, какие технологии данные @#\$%^ используют.

"При разработке собственных продуктов в 0day technologies применются самые актуальные на сегодняшний день технологии: Anomaly Detection; Association Rule Learning; Classification; Clustering; Data Mining; Deep Data Analysis; Deep Learning; Deep Packet Inspection; Machine Learning; Massively Parallel Processing; Natural Language Processing; OLAP; Sentimental Analysis; Regression; Behaviour nalysis; Signature Analysis."

Взято из "Каталог продуктов 0day technologies"

<a href="https://theins.ru/politika/154131" rel="nofollow">Подробнее</a>.

Хм. как интересно, взял их документ, маркированный как "строго конфиденциально" и отправил в министерство и в МГУ.

<br/>

### Специалист по поиску кадров в интернете, прислал вакансии по интересующим меня направлениям работы

Но не взяли. Помурыжили с неделю мозги, а потом сказали, что раз у меня нет опыта (а я нигде этого и не писал) работы с блокчей платформами, они отказывают мне даже в собеседовании.

Зарплата достойная. Место работы Сочи. Что за работодатель не знаю. Но требования к соискателям можно использовать для изучения того, в каком направлении следует развиваться.

Upd. Я думаю, что это

Филиал - R&D-центр, одной из крупнейших Российских ИТ компании «ОЦРВ» в г. Сочи, работающий по направлениям разработки ПО, моделированию процессов и созданию обучающих тренажеров виртуальной реальности для ОАО «РЖД».

Собственно <a href="/files/jobs.xlsx">позиции</a>. (Excel документ).

<br/>

**Для контактов:**

email:

![Marley](/img/a3333333mail.gif 'Marley')
