---
layout: page
title: Hyperleger Fabric - Writing Your First Application
description: Hyperleger Fabric - Writing Your First Application
keywords: Blockchain, Hyperleger, Fabric, Официальная документация, Writing Your First Application
permalink: /blockchain/hyperledger/fabric/official-docs/tutorials/writing-your-first-application/
---

# 7.2 Hyperleger Fabric - Writing Your First Application

Делаю:

26.08.2020

<br/>

### Все удаляю

    $ docker stop logspout
    $ docker rm logspout
    $ ./network.sh down

<br/>

    $ {
        docker stop $(docker ps -aq)
        docker rm $(docker ps -aq)
        docker system prune -a
    }

    $ cd ~/projects/dev/hyperledger/
    $ sudo rm -rf *

<br/>

    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s

<br/>

Работаем с fabric-samples/asset-transfer-basic

У нас есть:

- Приложение на javascript (asset-transfer-basic/application-javascript)
- Smart Contract на javascript, java, go, typescript (chaincode-\*)

<br/>

### 1. Setting up a development environment

    $ cd fabric-samples/test-network/

    // This command will deploy the Fabric test network with two peers, an ordering service, and three certificate authorities (Orderer, Org1, Org2). Instead of using the cryptogen tool, we bring up the test network using Certificate Authorities,
    hence the -ca flag. Additionally, the org admin user registration is bootstrapped when the Certificate Authority is started. In a later step, we will show how the sample application completes the admin enrollment.

    // Еще и не с первого раза запускается
    $ ./network.sh down && ./network.sh up createChannel -c mychannel -ca


    // This script uses the chaincode lifecycle to package, install, query installed chaincode, approve chaincode for both Org1 and Org2, and finally commit the chaincode.
    $ ./network.sh deployCC -ccn basic -ccl javascript

В общем мы завершили работу над backend.

<br/>

### Sample application

    $ cd ~/projects/dev/hyperledger/
    $ cd fabric-samples/asset-transfer-basic/application-javascript/
    $ npm install

    $ node app.js



<br/>

### 2. Explore a sample smart contract

<br/>

### 3. Interact with the smart contract with a sample application
