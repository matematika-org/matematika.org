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
    $ ./network.sh down && ./network.sh up createChannel -c mychannel -ca

<br/>

    $ docker ps
    CONTAINER ID        IMAGE                               COMMAND             CREATED              STATUS              PORTS                              NAMES
    a5f40dd145b3        hyperledger/fabric-peer:latest      "peer node start"   About a minute ago   Up About a minute   0.0.0.0:7051->7051/tcp             peer0.org1.example.com
    ed0386bf2432        hyperledger/fabric-peer:latest      "peer node start"   About a minute ago   Up About a minute   7051/tcp, 0.0.0.0:9051->9051/tcp   peer0.org2.example.com
    aded9b9ab1d3        hyperledger/fabric-orderer:latest   "orderer"           About a minute ago   Up About a minute   0.0.0.0:7050->7050/tcp             orderer.example.com

<br/>

### Скачиваю проект

    $ cd ~/projects/dev/hyperledger

    $ git clone https://github.com/webmakaka/Blockchain-for-Business-with-Hyperledger-Fabric

<br/>

### Chaincode

    $ cd /home/marley/projects/dev/hyperledger/Blockchain-for-Business-with-Hyperledger-Fabric/app/chaincode
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
