---
layout: page
title: Rajeev Sakhuja - Mastering Hyperledger Chaincode Development using GoLang
description: Rajeev Sakhuja - Mastering Hyperledger Chaincode Development using GoLang
keywords: Blockchain, Hyperleger, Fabric, Mastering Hyperledger Chaincode Development using GoLang
permalink: /videos/blockchain/hyperledger/en/fabric/mastering-hperledger-chaincode-development-using-golang/
---

# [Rajeev Sakhuja] Mastering Hyperledger Chaincode Development using GoLang [ENG, 2019, Latest updates 16/06/2020]

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

Автор написал свои скрипты и мы (по крайней мере по началу) дергаем их. Также у начале используем какой-то его готовы пример, что он делает непонятно. (Надеюсь по началу).

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

## 05. Fabric 2.x Chaincode Lifecycle

<br/>

### 02. Exercise- Chaincode Packaging & Installation

cahin.sh package - создает пакет
chain.sh install - инсталлирует пакет
chian.sh install -p - создает а потом инсталлирует default пакет

<br/>

    $ dev-init.sh
    $ source  set-env.sh  acme
    $ chain.sh package -o
    $ chain.sh package
    $ ls ${HOME}/packages

<br/>

    $ chain.sh install -p
    $ chain.sh queryinstalled

<br/>

### 04. Exercise - Chaincode Approval & Commitment

    $ dev-init.sh
    $ source  set-env.sh  acme
    $ chain.sh install -p

    $ chain.sh check
    $ chain.sh approve
    $ chain.sh check

    $ chain.sh querycommitted
    $ chain.sh commit
    $ chain.sh querycommitted
    $ chain.sh list

<br/>

    $ chain.sh instantiate -o
    $ set-chain-env.sh -I false
    $ chain.sh instantiate -o

<br/>

### 06. Exercise - Chaincode Invoke & Query

```
$ {
    dev-init.sh
    source  set-env.sh  acme
    chain.sh install -p
    chain.sh approve
    chain.sh commit
}
```

    $ chain.sh query
    $ chain.sh init -o
    $ chain.sh init
    $ chain.sh query

    $ chain.sh list
    $ set-chain-env.sh -q '{"Args": ["query", "a"]}'
    $ chain.sh query
    $ set-chain-env.sh -q '{"Args": ["query", "b"]}'
    $ chain.sh query
    $ set-chain-env.sh -i '{"Args": ["invoke", "a","b","s"]}

    // У меня ошибка. У автора все ОК.
    $ chain.sh invoke

    $ chain.sh query

<br/>

### 08. Exercise - Chaincode Upgrade

```
$ {
    dev-init.sh
    source  set-env.sh  acme
    chain.sh install -p
    chain.sh instantiate
}

```

    $ chain.sh list
    $ set-chain-env.sh -v 2.0
    $ chain.sh package
    $ chain.sh install
    $ chain.sh approve -o

    // s - sequence
    $ set-chain-env.sh -s 2
    $ chain.sh approve
    $ chain.sh commit
    $ chain.sh list

<br/>

    $ chain.sh queryinstalled
    $ chain.sh install -p
    $ chain.sh list
    $ chain.sh approve
    $ chain.sh upgrade-auto
    $ chain.sh list

<br/>

### 09. Chaincode Net versus Dev Mode

    $ dev-init.sh -d
    $ source  set-env.sh acme
    $ set-chain-env.sh
    $ chain.sh install
    $ cc-run.sh

В отдельной сесссии

    $ source  set-env.sh acme
    $ chain.sh instantiate
    $ chain.sh invoke
    $ chain.sh query

<br/>

## 06. Go Chaincode Interface

<br/>

### 02. Logging from Chaincode

    $ go run acflogger/test

<br/>

### 03. Hands On Chaincode Install Commit Logging Walkthrough

Получение логов из контейнера

Terminal session 1

    $ dev-init.sh
    $ source  set-env.sh acme
    $ set-chain-env.sh -n token  -v 1.0  -p token/v2 -c '{"Args":["init"]}'
    $ chain.sh install -p
    $ chain.sh instantiate
    $ cc-logs.sh -f

Terminal session 2

    $ source  set-env.sh acme
    $ chain.sh invoke

При выполнении в первом терминале получаем сообщения.

<br/>

network/config/core.yaml

Устанавливаем logging level в error

```
    logging:
      # Default level for all loggers within the chaincode container
      level:  error
```

Terminal session 1

    $ dev-stop.sh
    $ dev-start.sh
    $ cc-logs.sh -f

Terminal session 2

    $ chain.sh invoke

В терминале 1 только сообщения об ошбках Error и Fatal

Вернули level: info

<br/>

### 04. Hands On Chaincode Interface

    $ dev-init.sh -e
    $ source set-env.sh acme
    $ set-chain-env.sh   -n  token   -p token/v1    -c '{"Args": ["init"]}'

    $ chain.sh package
    $ chain.sh install

    $ chain.sh approveformyorg
    $ chain.sh commit

http://localhost:8080/#/transactions

    $ cc-logs.sh -t 10 -f

Terminal session 2

    $ source set-env.sh acme
    $ chain.sh  init
    $ chain.sh  query
    $ chain.sh invoke
    $ chain.sh query

<br/>

### 05. Sending the Success & Error Response

    $ chain.sh install -p
    $ set-chain-env.sh -s 2
    $ chain.sh instantiate -n
    $ chain.sh invoke

<br/>

## 07. Go Chaincode Stub

    $ dev-init.sh
    $ source set-env.sh acme

    $ set-chain-env.sh -n token -p token/v3
    $ chain.sh install -p
    $ chain.sh instantiate
    $ cc-logs.sh -f

Terminal session 2

    $ source set-env.sh acme
    $ chain.sh invoke
    $ chain.sh query

<br/>

# Part-2

Разкомментили код в файле: v3/goken.go

    $ go get github.com/golang/protobuf/proto

<br/>

    $ chain.sh install-auto
    $ set-chain-env.sh -s 2
    $ chain.sh instantiate
    $ cc-logs.sh -f

Terminal session 2

    $ chain.sh invoke

<br/>

### 05. Hands On Using Arguments function

    $ dev-init.sh
    $ source set-env.sh acme
    $ cc-logs.sh -f

Terminal session 2

    $ set-chain-env.sh   -n token   -v 1.0   -p token/v4

    $ chain.sh install -p
    $ source  set-env.sh  acme
    $ chain.sh install -p
    $ chain.sh instantiate

    $ set-chain-env.sh   -i    '{"args":["func-name"]}'

    $ chain.sh invoke

    $ set-chain-env.sh   -i    '{"args":["func-name","param-1","param-2"]}'
    $ chain.sh   invoke

<br/>

### 08. Hands On Chaincode State Functions GetState, PutState & DelState

"token/v5/token.go"

    $ dev-init.sh
    $ source  set-env.sh acme
    $ set-chain-env.sh -n token -v 1.0 -p token/v5
    $ set-chain-env.sh   -i   '{"args":["set"]}' -q   '{"args":["get"]}'
    $ chain.sh install -p
    $ chain.sh instantiate
    $ chain.sh query
    $ chain.sh invoke

<br/>

### 09. Exercise Add the delete function to V5 Token implementation

"token/v5/token.go"

В token.go добавить

```
 else if(funcName == "delete"){
		return DeleteToken(stub)
	}
```

    $ dev-init.sh
    $ source  set-env.sh acme
    $ set-chain-env.sh -n token -v 1.0 -p token/v5
    $ set-chain-env.sh   -i   '{"args":["set"]}' -q   '{"args":["get"]}'
    $ chain.sh install -p
    $ set-chain-env.sh  -c  '{"args":[]}'
    $ chain.sh instantiate
    $ chain.sh query
    $ chain.sh invoke
    $ chain.sh query

<br/>

    $ set-chain-env.sh -i '{"args":["delete"]}'
    $ chain.sh invoke
    $ chain.sh query

<br/>

### 12. Hands On InvokeChaincode function

"token/v6/caller.go"

Terminal session 1

    $ chmod +x $GOPATH/src/token/v6/setup-cc.sh
    $ $GOPATH/src/token/v6/setup-cc.sh

<br/>
    
    $ source  set-env.sh acme
    $ set-chain-env.sh -n token
    $ cc-logs.sh -f

Terminal session 2

    $ source  set-env.sh acme
    $ set-chain-env.sh -n caller
    $ cc-logs.sh -f

Terminal session 3

    $ source  set-env.sh acme
    $ set-chain-env.sh  -n caller
    $ set-chain-env.sh  -n caller -i '{"args":["setOnCaller"]}'  -q '{"args":["getOnCaller"]}'
    $ chain.sh query
    $ chain.sh invoke
    $ chain.sh query

<br/>

### 15. Hands On Event function usage

"token/v8/token.go"

    $ dev-init.sh
    $ source  set-env.sh acme
    $ set-chain-env.sh  -n token -v 1.0 -p token/v8 -c '{"Args": ["init"]}'
    $ chain.sh install -p
    $ chain.sh instantiate

    $ events.sh -t chaincode -n token -e TokenValueChanged -c airlinechannel

Terminal session 2

    $ source  set-env.sh acme
    $ set-chain-env.sh   -i   '{"args":["set"]}' -q   '{"args":["get"]}'
    $ chain.sh invoke

<br/>

## 8. Writing Unit Test Cases for Network Applications
