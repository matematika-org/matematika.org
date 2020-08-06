---
layout: page
title: Hyperleger Fabric (Blockchain)
description: Hyperleger Fabric (Blockchain)
keywords: Blockchain, Hyperleger, Fabric
permalink: /blockchain/hyperledger/fabric/
---

# Hyperleger Fabric (Blockchain)

<br/>

### [Rajeev Sakhuja] Mastering Hyperledger Chaincode Development using GoLang [ENG, 2019, Latest updates 16/06/2020]

Язык вроде норм. Лучше большинства индусов.

Автор обновил курс до Fabric 2.1. Уметь работать с Fabric 1.X не требуется.

**Сайт автора:**  
http://www.bcmentors.com/courses/

<br/>

Странный этот индус какой-то.

**Код для проекта:**  
http://www.bcmentors.com/download/hlf-dev-chaincode-v1-4-1-zip/

**Пароль:**
04-25-2020

**Fabric 2.0 Sample Chaincode used in the course by Raj.**  
https://github.com/acloudfan/HLF-GO-2.0

<br/>

2 способа развернуть оружение:

- простой - с помощью подготовленной виртуалки и скриптов
- самостоятельно все настраивать. (Может когда понадобится, тогда и посмотрим).

<br/>

### Простой - с помощью подготовленной виртуалки и скриптов

Виртуалка качалась 3 часа.

<br/>

    $ cd HLF-Dev-Chaincode-V2.1-1.0

<br/>

    $ vi Vagrantfile

```
# 1. Use this for "Standard setup"
# config.vm.box = "bento/ubuntu-18.04"

# 2. Use this for "VirtualBox Express Setup"
config.vm.box = "acloudfan/hlfdev2.0-0"
```

<br/>

    $ vagrant up

    // password vagrant
    $ vagrant ssh

<br/>

    $ cd network/setup/vexpress/
    $ chmod +x ./init-vexpress.sh
    $ ./init-vexpress.sh


    $ cd network/setup/
    $ chmod +x ./validate-setup.sh
    $ ./validate-setup.sh

    $ chmod +x ./update-git-repo.sh
    $ ./update-git-repo.sh

<br/>

    $ cd network/bin/
    $ chmod +x *

    $ dev-init.sh

    // $ dev-start.sh

    $ docker ps

    $ dev-validate.sh

    $ dev-validate.sh skip

    $ dev-mode.sh

    $ dev-stop.sh

<br/>

### 6. Hands On Setting the environment & executing peer commands

    $ source set-env.sh  acme
    // $ source set-env.sh  budget

    $ show-env.sh

    // Чтобы обновить
    $ export FABRIC_LOGGING_SPEC=debug

    $ show-env.sh

<br/>

    $ export  FABRIC_LOGGING_SPEC=info

    $ peer channel list

    $ export  FABRIC_LOGGING_SPEC=error

    $ peer channel getinfo -c airlinechannel

    $ peer lifecycle chaincode queryinstalled

<br/>

### HyperLedger Explorer

    $ dev-init.sh -e

    http://localhost:8080/

    $ dev-stop.sh

<br/>

### 8. Hands On Chaincode execution utility

    $ set-chain-env.sh
    $ show-chain-env.sh

    $ reset-chain-env.sh

    $ source set-env.sh acme
    $ chain.sh queryinstalled
    $ chain.sh query
    $ chain.sh invode -o

    copy command and paste

    $ chain.sh querycommitted -o

<br/>

### [Packt, Mayank Vijh] The Complete Hyperledger Fabric Fundamentals Course [ENG (Индус), 2018]

Наверное, устарело
