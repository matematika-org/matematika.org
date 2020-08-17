---
layout: page
title: Nakul Shah - Blockchain for Business with Hyperledger Fabric
description: Nakul Shah - Blockchain for Business with Hyperledger Fabric
keywords: Blockchain, Hyperleger, Fabric, Nakul Shah, Blockchain for Business with Hyperledger Fabric
permalink: /books/blockchain/hyperledger/en/fabric/blockchain-for-business-with-hyperledger-fabric/
---

# [Nakul Shah] Blockchain for Business with Hyperledger Fabric: A complete guide to enterprise Blockchain implementation using Hyperledger Fabric [ENG, 2019]

Если кто будет изучать, присоединяйтесь. Может у вас лучше получится и вы подскажете как сделать, чтобы работало.

<br/>

### VS Code extension: IBM Blockchain Platform

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

## Frameworks, Network Topologies, and Modeling

<br/>

Fabric uses a very powerful and modern stack of technology that makes it robust.

Some of these technologies include the following:

1. Docker as a containerization technology
2. Node.js for chaincode and client application
3. Golang for chaincode and for Fabric itself

<br/>

Configuration files:

a. configtx.yml
b. crypto-config.yml
c. docker-compose files

<br/>

### Process of creating Hyperledger network

Добавить 125 стр.

<br/>

Убеждаемся что необходимые программы установлены:

    $ docker -v
    $ docker-compose -v
    $ go version

<br/>

### Поехали

    $ cd ~/projects/dev/
    $ mkdir -p hyperledger && cd hyperledger
    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s 1.4.0

<!--
1.4.8
-->

What does this script do?

a. It clones the Fabric sample repo we discussed earlier, the same you have in your editor.

b. Then it pulls the binaries that we discussed, like confitxgen, cryptogen, and so on, and puts them in the bin folder inside the fabric-sample folder cloned in the last step.

c. It then pulls all the images and tags them with the version that we provided, i.e., 1.4.0.

<!--

    $ git clone https://github.com/hyperledger/fabric-samples.git

-->

<br/>

$ cd fabric-samples/bin/
$ ls

```
configtxgen    cryptogen  fabric-ca-client  get-docker-images.sh  orderer
configtxlator  discover   fabric-ca-server  idemixgen             peer
```

<br/>

    $ pwd

/home/marley/projects/dev/hyperledger/fabric-samples/bin

<br/>

    $ export PATH=/home/marley/projects/dev/hyperledger/fabric-samples/bin/:$PATH

<br/>

    // Проверка
    $ cryptogen --help

<br/>

### 2. Generate crypto material and channel configuration files

We need to write crypto-config.yaml

    $ cd ../first-network/
    $ cryptogen generate --config=./crypto-config.yaml

Now you should see a folder crypto-config generated in the first-network directory.

<br/>

### 3. Start the network using Docker Compose YAML

Next, we need to write configtx.yaml to generate the channel-related artefacts in YAML.

    // we need to generate the artefacts for the orderer system channel, which is required for the orderer to work properly
    $ configtxgen -profile TwoOrgsOrdererGenesis -channelID byfn-sys-channel -outputBlock ./channel-artifacts/genesis.block

    $ ls ./channel-artifacts/genesis.block

<br/>

    // generate channel.tx file using the configuration defined in twoOrgsChannel
    $ configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID testchannel

<br/>

    // generate a TX file for the anchor peers in the channel

    // Org1
    $ configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID testchannel -asOrg Org1MSP

    // Org2
    $ configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID testchannel -asOrg Org2MSP

<br/>

    $ ls ./channel-artifacts/
    channel.tx  genesis.block  Org1MSPanchors.tx  Org2MSPanchors.tx

<br/>

### 4. Start the network using Docker Compose files.

    $ IMAGE_TAG=1.4.0 docker-compose -f docker-compose-cli.yaml up -d

<!--
    $ IMAGE_TAG=latest docker-compose -f docker-compose-cli.yaml up -d
-->

Создаются следующие peer

```
peer0.org1.example.com
peer1.org1.example.com
peer0.org2.example.com
peer1.org2.example.com
```

+

orderer.example.com

<br/>

### При необходимости удалить контейнеры, чтобы пересоздать

    $ cd fabric-samples/first-network

    // остановить docker-compose и удалить все
    $ docker-compose -f docker-compose-cli.yaml down --volumes

<!--

<br/>

### 5. Create channels and install, instantiate, and query chaincode.

    $ docker exec -it cli bash

    $ peer channel create -o orderer.example.com:7050 -c dummyChannel -f ./channel-artifacts/channel.tx

-->

**Для инсталляция chaincode из примеров на разных языках:**

    // golang - ok
    $ docker exec cli scripts/script.sh testchannel 3 golang 10 true

    // node - ошибка
    $ docker exec cli scripts/script.sh testchannel 3 node 10 true

    // java - ошибка
    $ docker exec cli scripts/script.sh testchannel 3 node 10 true

<br/>

```
Error: could not assemble transaction, err proposal response was not successful, error code 500, msg timeout expired while starting chaincode mycc:1.0 for transaction
!!!!!!!!!!!!!!! Chaincode instantiation on peer0.org2 on channel 'testchannel' failed !!!!!!!!!!!!!!!!
========= ERROR !!! FAILED to execute End-2-End Scenario ===========
```

<br/>

Похоже или я неправильно что-то делаю, или тестовые примеры работают только с кодом на языке GoLang.

Если разберусь как все это работает, может удастся победить.

<!--

https://hyperledger-fabric.readthedocs.io/en/release-1.4/build_network.html

-->

<br/>

### Install Node.js chaincode (Не заработало!)

Now let’s try to run install chaincode from the Node.js chaincode available in chaincode/chaincode_example02/node/

    $ docker exec -it cli bash

    # echo $CORE_PEER_LOCALMSPID
    Org1MSP

    # echo $CORE_PEER_ADDRESS
    peer0.org1.example.com:7051

<br/>

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

    # export CORE_PEER_ADDRESS=peer1.org1.example.com:7051

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

**Let’s change the env variables**

    # CORE_PEER_LOCALMSPID="Org2MSP"

    # CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp

    # CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt

<br/>

    # CORE_PEER_ADDRESS=peer0.org2.example.com:7051

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

**Повторяем**

    # CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer1.org2.example.com/tls/ca.crt

    # CORE_PEER_ADDRESS=peer1.org2.example.com:7051

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

### Instantiate the chaincode

    # ctrl ^D
    $ docker exec -it cli bash

<br/>

    # peer chaincode instantiate -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n testcc -l node -v 1.1 -c '{"Args":["init","a","100","b","200"]}' -P "AND ('Org1MSP.peer','Org2MSP.peer')"

Ошибка!!!

<br/>

**Повторить для:**

    # CORE_PEER_ADDRESS=peer0.org1.example.com:7051

    # CORE_PEER_ADDRESS=peer1.org1.example.com:7051

    # CORE_PEER_ADDRESS=peer0.org2.example.com:7051

    # CORE_PEER_ADDRESS=peer1.org2.example.com:7051

<br/>

    # peer channel list

<br/>

### 3. Query the chaincode:

    # peer chaincode query -C mychannel -n testcc -c '{"Args":["query","a"]}'

This should give output as 100.

<br/>

### 4. Upgrade the chaincode:

    # peer chaincode install -n testcc -v 1.3 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

For testing instead of installing in all the nodes, we will upgrade only in peer0 by using the below command:

    # peer chaincode upgrade -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n testcc -l node -v 1.3 -c '{"Args":["init","a","90","b","200"]}' -P "AND ('Org1MSP.peer','Org2MSP.peer')"

Ошибка !!!

    # peer chaincode query -C mychannel -n testcc -c '{[" a"]}'

Наверное должно быть

    # peer chaincode query -C mychannel -n testcc -c '{"Args":["a"]}'

This will now show 90.

<br/>

## Frameworks, Network Topologies, and Modeling
