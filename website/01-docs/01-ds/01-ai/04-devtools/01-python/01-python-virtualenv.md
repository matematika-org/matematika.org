---
layout: page
title: Virtualenv
description: Подготовка виртуального окружения для запуска python приложение в изолированной среде
keywords: python, virtualenv
permalink: /ds/ai/devtools/python/virtualenv/
---

# Virtualenv

**Скорее всего, не следует заменять python на версию по умолчанию 3, т.к. некоторые программы, могут перестать работать правильно. Но это дело каждого.**

С версией 3.8 не заработал jupyter из коробки. Наверное, тоже нужно было установить pexpect.

```python
$ sudo apt-get update && sudo apt-get upgrade -y
$ sudo apt-get install -y python3.7

$ sudo apt-get install -y virtualenv

$ ls /usr/bin/python3.7

// Приоритет 1
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.7 1
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 1


// Не нужон он нам ваш python версии 2.
$ update-alternatives --list python
$ update-alternatives --list python3

$ sudo update-alternatives --config python
$ sudo update-alternatives --config python3


Новое окно

$ python --version
Python 3.7.5


$ python3 --version
Python 3.7.5

```

<br/>

### Запуск jupyter notebook и стандартных библиотек

```python

$ mkdir -p ~/projects/dev/ml
$ cd ~/projects/dev/ml

$ mkdir handson-ml && cd handson-ml

$ virtualenv --system-site-packages -p python handson-ml-env
$ source handson-ml-env/bin/activate

$ pip install --upgrade pip

$ {
    pip install --upgrade jupyter
    pip install --upgrade matplotlib
    pip install --upgrade numpy
    pip install --upgrade pandas
    pip install --upgrade scipy
    pip install --upgrade scikit-learn
}


// Без этого пакета ошибка
// def expect(self, pattern, timeout=-1, searchwindowsize=-1, async=False):
$ pip install --upgrade pexpect


<br/>

    $ jupyter notebook --ip 0.0.0.0 --port 8888

```

<br/>

```python
import matplotlib
import numpy
import pandas
import scipy
import sklearn


print('matplotlib',  matplotlib.__version__)
print('numpy', numpy.__version__)
print('pandas', pandas.__version__)
print('scipy', scipy.__version__)
print('sklearn', sklearn.__version__)

```

```
matplotlib 3.2.2
numpy 1.19.0
pandas 1.0.5
scipy 1.5.1
sklearn 0.23.1
```

<br/>

### Всевозможное примеры для запуска Tensorflow 2

<!--

    $ pip install yolk3k
    $ yolk -V tensorflow

-->

    $ pip install --upgrade tensorflow==2.0.0

```
(tf_2) $ python -c "import tensorflow as tf; x = [[2.]]; print('tensorflow version', tf.__version__); print('hello, {}'.format(tf.matmul(x, x)))"
```

    $ pip install jupyterlab

    $ mkdir -p ~/jupyter
    $ cd ~/jupyter

    $ jupyter notebook --ip 0.0.0.0 --port 8888

<br/>

http://<jupyter_host>:8888

Посмотреть в консоли token.

<br/>

```

from platform import python_version
print('python: ' + python_version())

import tensorflow as tf
print('tf: ' + tf.__version__)

```

python: 3.6.8
tf: 2.0.0

Все ок.
