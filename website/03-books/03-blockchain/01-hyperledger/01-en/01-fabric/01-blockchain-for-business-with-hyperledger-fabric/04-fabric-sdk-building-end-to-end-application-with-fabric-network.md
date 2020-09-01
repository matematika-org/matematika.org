---
layout: page
title: Nakul Shah - Blockchain for Business with Hyperledger Fabric - Fabric SDK Building End-to-End Application with Fabric Network
description: Nakul Shah - Blockchain for Business with Hyperledger Fabric - Fabric SDK Building End-to-End Application with Fabric Network
keywords: Blockchain, Hyperleger, Fabric, Nakul Shah, Blockchain for Business with Hyperledger Fabric, Fabric SDK
permalink: /books/blockchain/hyperledger/en/fabric/blockchain-for-business-with-hyperledger-fabric/fabric-sdk-building-end-to-end-application-with-fabric-network/
---

# [Nakul Shah] Blockchain for Business with Hyperledger Fabric: A complete guide to enterprise Blockchain implementation using Hyperledger Fabric [ENG, 2019]

<br/>

## Fabric SDK: Building End-to-End Application with Fabric Network

<br/>

# НЕ РАБОТАЕТ!!!

<br/>

### Переключился на node v12

    $ {
      nvm install v12.18.3
      nvm use v12.18.3
      nvm alias default v12.18.3
    }

<br/>

### Все удаляю

    $ cd ~/projects/dev/hyperledger/
    $ sudo rm -rf *

<br/>

    $ {
        docker stop $(docker ps -aq)
        docker rm $(docker ps -aq)
        docker system prune -a
    }

<br/>

    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s

<br/>

    $ cd /home/marley/projects/dev/hyperledger/fabric-samples/test-network/

<!--
    $ export FABRIC_CA_SERVER_CA_NAME=ca1.example.com

    ca1.example.com
    ca2.example.com

    ca.org1.example.com
-->

    $ ./network.sh down && ./network.sh up createChannel -c mychannel -ca

<br/>

    $ docker ps
    CONTAINER ID        IMAGE                               COMMAND                  CREATED             STATUS              PORTS                              NAMES
    b68320e99da8        hyperledger/fabric-peer:latest      "peer node start"        33 seconds ago      Up 30 seconds       7051/tcp, 0.0.0.0:9051->9051/tcp   peer0.org2.example.com
    d856a59deaaa        hyperledger/fabric-orderer:latest   "orderer"                33 seconds ago      Up 31 seconds       0.0.0.0:7050->7050/tcp             orderer.example.com
    c7228c77e6c0        hyperledger/fabric-peer:latest      "peer node start"        33 seconds ago      Up 31 seconds       0.0.0.0:7051->7051/tcp             peer0.org1.example.com
    1c9f53523d6d        hyperledger/fabric-ca:latest        "sh -c 'fabric-ca-se…"   52 seconds ago      Up 50 seconds       0.0.0.0:7054->7054/tcp             ca_org1
    938938a0088d        hyperledger/fabric-ca:latest        "sh -c 'fabric-ca-se…"   52 seconds ago      Up 50 seconds       7054/tcp, 0.0.0.0:9054->9054/tcp   ca_orderer
    473359ec9851        hyperledger/fabric-ca:latest        "sh -c 'fabric-ca-se…"   52 seconds ago      Up 49 seconds       7054/tcp, 0.0.0.0:8054->8054/tcp   ca_org2

<br/>

### Скачиваю проект

    $ cd ~/projects/dev/hyperledger

    $ git clone https://github.com/webmakaka/Blockchain-for-Business-with-Hyperledger-Fabric

<br/>

### Chaincode

    $ cd /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/chaincode

<!--


    $ npm install -g npm-check-updates
    $ ncu -u
    $ npm install


-->

    $ npm install
    $ npm run build

<br/>

    $ cd /home/marley/projects/dev/hyperledger/fabric-samples/test-network/

    $ {
        export PATH=${PWD}/../bin:$PATH
        export FABRIC_CFG_PATH=$PWD/../config/
    }

    $ peer lifecycle chaincode \
        package basic.tar.gz \
        --path /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/chaincode/ \
        --lang node \
        --label basic_1.0

Создался basic.tar.gz в текущем каталоге.

<br/>

### 7.1.4 Install the chaincode package

**Org1**

    $ {
        export CORE_PEER_TLS_ENABLED=true
        export CORE_PEER_LOCALMSPID="Org1MSP"
        export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
        export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
        export CORE_PEER_ADDRESS=localhost:7051
    }

<br/>

    $ peer lifecycle chaincode install basic.tar.gz

<br/>

**Org2**

    $ {
        export CORE_PEER_LOCALMSPID="Org2MSP"
        export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
        export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
        export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
        export CORE_PEER_ADDRESS=localhost:9051
    }

<br/>

    $ peer lifecycle chaincode install basic.tar.gz

<br/>

### 7.1.5 Approve a chaincode definition

    $ peer lifecycle chaincode queryinstalled

    // Будет отличаться от того, что у меня
    $ export CC_PACKAGE_ID=basic_1.0:4ec191e793b27e953ff2ede5a8bcc63152cecb1e4c3f301a26e22692c61967ad

    $ echo $CC_PACKAGE_ID

    $ peer lifecycle chaincode approveformyorg \
        -o localhost:7050 \
        --ordererTLSHostnameOverride orderer.example.com \
        --channelID mychannel \
        --name basic \
        --version 1.0 \
        --package-id $CC_PACKAGE_ID \
        --sequence 1 \
        --tls \
        --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem

<br/>

You need to approve a chaincode definition with an identity that has an admin role.

    $ {
        export CORE_PEER_LOCALMSPID="Org1MSP"
        export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
        export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
        export CORE_PEER_ADDRESS=localhost:7051
    }

<br/>

    $ peer lifecycle chaincode approveformyorg \
        -o localhost:7050 \
        --ordererTLSHostnameOverride orderer.example.com \
        --channelID mychannel \
        --name basic \
        --version 1.0 \
        --package-id $CC_PACKAGE_ID \
        --sequence 1 \
        --tls \
        --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem

<br/>

### 7.1.6 Committing the chaincode definition to the channel

    $ peer lifecycle chaincode checkcommitreadiness \
        --channelID mychannel \
        --name basic \
        --version 1.0 \
        --sequence 1 \
        --tls \
        --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem \
        --output json

<br/>

```
{
	"approvals": {
		"Org1MSP": true,
		"Org2MSP": true
	}
}

```

<br/>

    $ peer lifecycle chaincode commit \
        -o localhost:7050 \
        --ordererTLSHostnameOverride orderer.example.com \
        --channelID mychannel \
        --name basic \
        --version 1.0 \
        --sequence 1 \
        --tls \
        --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem \
        --peerAddresses localhost:7051 \
        --tlsRootCertFiles ${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt \
        --peerAddresses localhost:9051 \
        --tlsRootCertFiles ${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt

You can use the peer lifecycle chaincode querycommitted command to confirm that the chaincode definition has been
committed to the channel.

    $ peer lifecycle chaincode querycommitted \
        --channelID mychannel \
        --name basic \
        --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem

```
Committed chaincode definition for chaincode 'basic' on channel 'mychannel':
Version: 1.0, Sequence: 1, Endorsement Plugin: escc, Validation Plugin: vscc, Approvals: [Org1MSP: true, Org2MSP: true]

```

<br/>

### API

    $ cd /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/api

<!--

    $ mv enrollAdmin.js enrollAdmin.js.orig
    $ mv registerUser.js registerUser.js.orig

    $ cd /home/marley/projects/dev/hyperledger/fabric-samples


    $ sudo cp -r test-network/ /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric


    $ cd /home/marley/projects/dev/hyperledger/fabric-samples/fabcar/javascript

    $ cp enrollAdmin.js /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/api

    $ cp registerUser.js /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/api


    $ cd /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/api

    $ npm install fabric-network

      enrollmentID: 'user1',
      enrollmentSecret: secret,

-->

    $ npm install
    $ node enrollAdmin.js
    $ node registerUser.js

    $ npm start

<br/>

<br/>

### Client (angular)

    $ cd /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/client

    $ npm install
    $ npm start

http://localhost:4200/
