---
layout: page
title: Nakul Shah - Blockchain for Business with Hyperledger Fabric
description: Nakul Shah - Blockchain for Business with Hyperledger Fabric
keywords: Blockchain, Hyperleger, Fabric, Nakul Shah, Blockchain for Business with Hyperledger Fabric
permalink: /books/blockchain/hyperledger/en/fabric/blockchain-for-business-with-hyperledger-fabric/
---

# [Nakul Shah] Blockchain for Business with Hyperledger Fabric: A complete guide to enterprise Blockchain implementation using Hyperledger Fabric [ENG, 2019]

Если кто будет изучать, присоединяйтесь. Может у вас лучше получится и вы подскажете как сделать, чтобы работало.

За индусом нужен глаз да глаз. То там где-то напутает, то сям.
А вообще этот мудазвон заставил меня копипастить код из pdf. И только в следующей главе, он дал ссылку на репо, где хранится код.

К сожалению исходных кодов к книге нет. Да еще и при копи пасте команды в консоли не выполняются и необходимо предварительно их в техкстовом редакторе подправлять.

<br/>

### VS Code extension: IBM Blockchain Platform

Install the VSCode and IBM Blockchain Platform called VSCode extension.

• Use the keyboard shortcut Shift + CMD + P to bring up the command palette and select IBM Blockchain Platform: Create Smart Contract Project from the dropdown.

• Click JavaScript from the dropdown.
• Create a new folder and name it whatever you want, e.g., TestContract.
• Start by creating a new folder and open it. Next, from the dropdown on left top, click Add to Workspace.
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

**Код лежит здесь (чтобы не копипастить из pdf):**  
https://github.com/SateDev/hyperledger_chaincode_asset_registry

<br/>

The requirements are simple—we need to write a smart contract that will register
the property details, change the ownership, query the property details, and execute
a few other operations on the properties.

<br/>

We are going to build an asset registry chaincode application that has the following common attributes linked to a property:

    • Value of the property
    • Owner of the property
    • Property area
    • Location of the property
    • Type of property

<br/>

Now, let’s understand what we want this chaincode to do:

1. Create an initial ledger with some initial property details.
2. Provide functionality to create more properties using the “Create a Property” function.
3. Query the ledger for a property on the basis of property ID.
4. Allow querying all the properties on the basis of indexes.
5. Allow changing the owner of a property.

<br/>

https://fabric-shim.github.io/release-1.4/fabric-shim.ChaincodeStub.html

<br/>

### Deploying and testing the chaincode

<br/>

    $ npm i -g typescript

<br/>

    $ cd /home/marley/projects/dev/hyperledger

Терминал 1:

    $ {
        docker stop $(docker ps -aq)
        docker rm $(docker ps -aq)
        docker system prune -a
    }

    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s 1.2.1

    $ cd fabric-samples/chaincode

    $ mkdir asset-registry
    $ cd asset-registry

    $ git clone https://github.com/SateDev/hyperledger_chaincode_asset_registry .

<br/>

    $ cd /home/marley/projects/dev/hyperledger/fabric-samples/chaincode-docker-devmode
    $ docker-compose -f docker-compose-simple.yaml up

Не нужно ждать, можно сразу переключаться на другой терминал.

<br/>

Терминал 2:

    $ docker exec -it chaincode bash

    # cd asset-registry
    # npm install
    # npm run build
    # npm run start -- --peer.address "peer:7052" "--chaincode-id-name" "asset-cc:0.1"

```
Command succeeded

2020-08-18T03:37:25.887Z info [shim:lib/handler.js]                               Successfully registered with peer node. State transferred to "established"
2020-08-18T03:37:25.888Z info [shim:lib/handler.js]                               Successfully established communication with peer node. State transferred to "ready"

```

Our chaincode is now listening for any requests for peers and bash containers in
order to run operations.

<br/>

### Installing, instantiating, and invoking the chaincode:

Терминал 3:

    $ docker exec -it cli bash

    # peer chaincode install -p chaincode/asset-registry/ -n asset-cc -l node -v 0.1

```
2020-08-18 03:43:28.457 UTC [chaincodeCmd] install -> INFO 05c Installed remotely response:<status:200 payload:"OK" >
```

<br/>

    // Init
    # peer chaincode instantiate \
        -n asset-cc \
        -v 0.1 \
        -l node \
        -c '{"Args":["initLedger"]}' \
        -C myc

Ok

<br/>

    // Найти по ID
    # peer chaincode query \
        -n asset-cc \
        -c '{"Args":["queryAsset", "P100001"]}' \
        -C myc

Ok

<br/>

    // createProperty:
    # peer chaincode invoke \
        -n asset-cc \
        -c '{"Args":["createProperty", "P100003", "howbe", "2838", "somehg", "asdf", "2323", "someowner"]}' \
        -C myc

Ok

    // change the owner
    # peer chaincode invoke \
        -n asset-cc \
        -c '{"Args":["changePropertyOwner", "P100003", "marley"]}' \
        -C myc

Ok

    # peer chaincode query \
        -n asset-cc \
        -c '{"Args":["queryAsset", "P100003"]}' \
        -C myc

Ok

<br/>

Дальше у меня было не все хорошо с расширением для vscode.

<br/>

## Fabric SDK: Interaction with Fabric Network

    // Репо ушло вперед. Использую другой вариант. В книге предлагают
    // $ git clone https://github.com/hyperledger/fabric-samples.git

    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s 1.4.0

    $ cd fabric-samples

It is a one-organization network comprising one peer, one orderer, Fabric CA, CouchDB, and CLI container.

    $ cd chaincode

    $ mkdir asset-registery
    $ cd asset-registery

    $ git clone https://github.com/SateDev/hyperledger_chaincode_asset_registry .

    // Ошибка дальше, если не выполнить. (На моем ПК)
    // "Duplicate identifier 'IteratorResult'"
    $ npm update --save-dev @types/node

<br/>

    $ cd ../

    $ mkdir startup
    $ cd startup

    $ curl -OL https://raw.githubusercontent.com/SateDev/asset-registry-sdk/master/scripts/startup.sh

<br/>

    $ chmod 777 ./startup.sh
    $ ./startup.sh typescript

<br/>

<br/>

### Enrolment and registration of admin and user

using CA server

    $ cd ~/projects/dev/hyperledger/

    $ git clone https://github.com/SateDev/asset-registry-api

    $ cd asset-registry-api

    $ code .

Заменить во всем проекте 52.187.123.234 на localhost

    $ npm install
    $ node enrollAdmin.js

This will fetch the certificates from the CA server and put them in the path

Создается каталог hfc-key-store с приватным и публичным ключом.

    $ ls ./hfc-key-store/
    37f942a7a1440f93a980c2273e15898e390738ebcb99e9d139eac8766343cf74-priv
    37f942a7a1440f93a980c2273e15898e390738ebcb99e9d139eac8766343cf74-pub
    6adf7f30861af5ec871e3935e124902df33235106474f9e53a6e53749f16c1bc-priv

<br/>

### Registration and enrolment of the user

    $ node registerUser.js

В hfc-key-store добавились ключи для созданного пользователя.

<br/>

### Chaincode invoke and query

Как сделал индус, из коробки у меня не заработало.

Я вынес функцию invoke и вызвал ее.

```
invoke();


async function invoke(p,r,o,m,a,i,n) {
```

    $ node invoke.js

Походу всеравно ошибка.

```
Start invoke processing

Created a transaction ID: 8e3ee6926d1e0f4b694754ffd343aff36a7ab608f149c6e77d3df7c04e6489ae
undefined undefined undefined undefined undefined undefined undefined
Unable to invoke ::TypeError: First argument must be a string, Buffer, ArrayBuffer, Array, or array-like object.
```

<br/>

    $ node query.js

Ну да

```
Store path:/home/marley/projects/dev/hyperledger/asset-registry-api/hfc-key-store
Successfully loaded user1 from persistence
Failed to query successfully :: ReferenceError: start is not defined
```

<br/>

### Invoking ChangePropertyOwner from Fabric SDK

    $ node changeOwner.js
    $ node query.js

Вернусь и попробую победить, после завершения чтения книги.

<br/>

## Fabric SDK: Building End-to-End Application with Fabric Network

Настраиваем окружение как и в предыдущей главе.

    $ node enrollAdmin.js
    $ node registerUser.js
    $ node server.js

<br/>

Далее будем прикручивать angular приложение.

    $ cd ~/projects/dev/hyperledger/
    $ git clone https://github.com/SateDev/asset-registry-ui
    $ cd asset-registry-ui

Нужно в package.json поправить name. Чтобы было "name": "asset_registry". Иначе не запустится.

    $ npm install
    $ npm start

http://localhost:4200/

<br/>

## Fabric in Production

Не до production пока
