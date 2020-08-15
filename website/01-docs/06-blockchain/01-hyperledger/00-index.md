---
layout: page
title: Hyperleger (Blockchain)
description: Hyperleger (Blockchain)
keywords: Blockchain, Hyperleger
permalink: /blockchain/hyperledger/
---

# Hyperleger (Blockchain)

### Getting Started with Blockchain on GCP using Hyperledger Fabric and Composer

https://www.qwiklabs.com/focuses/3744?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=6510491

<!--

<br/>

VS Code extension: IBM Blockchain Platform

Install the VSCode and IBM Blockchain Platform called VSCode
extension.
• Use the keyboard shortcut Shift + CMD + P to bring up the command
palette and select IBM Blockchain Platform: Create Smart Contract
Project from the dropdown.
• Click JavaScript from the dropdown.
• Create a new folder and name it whatever you want, e.g., TestContract.
• Start by creating a new folder and open it. Next, from the dropdown on
left top, click Add to Workspace.
• Check the smart contract lib/my-contract.js in this location.

-->

<br/>

**Hyperledger tools**

- Hyperledger Explorer
- Hyperledger Cello
- Hyperledger Composer (deprecated)
- Hyperledger Caliper
- Hyperledger Quilt
- Hyperledger URSA

<br/>

### Fabric

Fabric 1.4 is the first production-ready LTS release.

    $ mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers
    $ curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz
    $ tar -xvf fabric-dev-servers.tar.gz
    $ cd ~/fabric-dev-servers
    $ ./downloadFabric.sh
    $ ./startFabric.sh

<br/>

    $ docker ps
    CONTAINER ID        IMAGE                               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    8e1a2c1aa4d8        hyperledger/fabric-peer:1.2.1       "peer node start"        25 seconds ago      Up 25 seconds       0.0.0.0:7051->7051/tcp, 0.0.0.0:7053->7053/tcp   peer0.org1.example.com
    8fb15bba185f        hyperledger/fabric-ca:1.2.1         "sh -c 'fabric-ca-se…"   29 seconds ago      Up 25 seconds       0.0.0.0:7054->7054/tcp                           ca.org1.example.com
    d8ee1e4ea551        hyperledger/fabric-orderer:1.2.1    "orderer"                29 seconds ago      Up 26 seconds       0.0.0.0:7050->7050/tcp                           orderer.example.com
    5f00c25178d2        hyperledger/fabric-couchdb:0.4.10   "tini -- /docker-ent…"   29 seconds ago      Up 25 seconds       4369/tcp, 9100/tcp, 0.0.0.0:5984->5984/tcp       couchdb

<br/>

    $ ./fabric-scripts/hlfv1/startFabric.sh

<br/>

### [Тестовое по Hyperledger](/blockchain/hyperledger/test-taks/)
