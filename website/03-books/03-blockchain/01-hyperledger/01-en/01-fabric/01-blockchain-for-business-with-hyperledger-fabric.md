---
layout: page
title: Nakul Shah - Blockchain for Business with Hyperledger Fabric
description: Nakul Shah - Blockchain for Business with Hyperledger Fabric
keywords: Blockchain, Hyperleger, Fabric, Nakul Shah, Blockchain for Business with Hyperledger Fabric
permalink: /books/blockchain/hyperledger/en/fabric/blockchain-for-business-with-hyperledger-fabric/
---

# [Nakul Shah] Blockchain for Business with Hyperledger Fabric: A complete guide to enterprise Blockchain implementation using Hyperledger Fabric [ENG, 2019]

Если кто будет изучать, присоединяйтесь. Может у вас лучше получится и вы подскажете как сделать, чтобы все работало.

За индусом нужен глаз да глаз. То там где-то напутает, то сям.
А вообще этот мудазвон заставил меня копипастить код из pdf. И только в следующей главе, он дал ссылку на репо, где хранится код.

К сожалению исходных кодов к книге нет. Да еще и при копи пасте команды в консоли не выполняются и необходимо предварительно их в текстовом редакторе подправлять.

Также мной были замечены ошибки в приведенных исходниках, как впрочем и в командах приведенных в книге.

<br/>

**Далее все будет запускаться в ubuntu 18 TLS.**

Редактор кода - vscode.

<br/>

Необходимы, чтобы были установлены следующие программы:

    $ docker -v
    $ docker-compose -v
    $ go version

<br/>

Также нужно установить node.js:

    -- installation

    $ LATEST_VERSION=$(curl --silent "https://api.github.com/repos/nvm-sh/nvm/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/')

    $ curl -o- https://raw.githubusercontent.com/creationix/nvm/${LATEST_VERSION}/install.sh | bash

<br/>

    $ export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

<br/>

    $ nvm --version
    0.35.3

Инсталляция подходящей версии node.js для проектов из книги.

    $ {
      nvm install v8.17.0
      nvm use v8.17.0
      nvm alias default v8.17.0
    }

<br/>

## Frameworks, Network Topologies, and Modeling

<br/>

**Configuration files:**

    a. configtx.yml
    b. crypto-config.yml
    c. docker-compose files

<br/>

### Подготовка окружения

    // Удаляю все контейнеры и имиджи докера, которые есть в системе.
    $ {
        docker stop $(docker ps -aq)
        docker rm $(docker ps -aq)
        docker system prune -a
    }

    $ mkdir -p ~/projects/dev/hyperledger

    $ cd ~/projects/dev/hyperledger/
    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s 1.4.8

<br/>

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

    $ cd ~/projects/dev/hyperledger/fabric-samples/first-network
    $ cryptogen generate --config=./crypto-config.yaml

Now you should see a folder crypto-config generated in the first-network directory.

<br/>

### 3. Start the network using Docker Compose YAML

Next, we need to write configtx.yaml to generate the channel-related artefacts in YAML.

    // we need to generate the artefacts for the orderer system channel, which is required for the orderer to work properly
    $ configtxgen \
        -profile TwoOrgsOrdererGenesis \
        -channelID byfn-sys-channel \
        -outputBlock ./channel-artifacts/genesis.block

    $ ls ./channel-artifacts/genesis.block

<br/>

    // generate channel.tx file using the configuration defined in twoOrgsChannel
    $ configtxgen \
        -profile TwoOrgsChannel \
        -outputCreateChannelTx ./channel-artifacts/channel.tx \
        -channelID mychannel

<br/>

    // generate a TX file for the anchor peers in the channel

    // Org1
    $ configtxgen \
        -profile TwoOrgsChannel \
        -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx \
        -channelID mychannel \
        -asOrg Org1MSP

    // Org2
    $ configtxgen \
        -profile TwoOrgsChannel \
        -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx \
        -channelID mychannel \
        -asOrg Org2MSP

<br/>

    $ ls ./channel-artifacts/
    channel.tx  genesis.block  Org1MSPanchors.tx  Org2MSPanchors.tx

<br/>

### 4. Start the network using Docker Compose files.

    $ IMAGE_TAG=1.4.8 docker-compose -f docker-compose-cli.yaml up -d

<br/>

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

    // При необходимости остановить docker-compose и удалить все
    // $ docker-compose -f docker-compose-cli.yaml down --volumes

<br/>

**Для инсталляция chaincode из примеров на разных языках:**

    // golang - ok
    $ docker exec cli scripts/script.sh mychannel 3 golang 10 true

    // node - ошибка
    $ docker exec cli scripts/script.sh mychannel 3 node 10 true

    // java - ошибка
    $ docker exec cli scripts/script.sh mychannel 3 node 10 true

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

Порты нужно смотреть в docker ps.

    $ docker exec -it cli bash

<!--

# apt update -y
# apt install -y  net-tools iputils-ping

# telnet peer0.org1.example.com 7051

-->

Вот такие у нас переменные окружения по умолчанию. P.S. Индус мудак и тот кто не проверял его писанину!

<br/>

**peer0.org1.example.com:7051**

    # echo $CORE_PEER_LOCALMSPID
    Org1MSP

    # echo $CORE_PEER_ADDRESS
    peer0.org1.example.com:7051

    # echo $CORE_PEER_TLS_ROOTCERT_FILE
    /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt

    # echo $CORE_PEER_MSPCONFIGPATH
    /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp

<br/>

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

**peer1.org1.example.com:8051**

    # export CORE_PEER_ADDRESS=peer1.org1.example.com:8051

    # export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer1.org1.example.com/tls/ca.crt

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

**peer0.org2.example.com:9051**

    # export CORE_PEER_LOCALMSPID="Org2MSP"

    # export CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp

    # export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt

<br/>

    # export CORE_PEER_ADDRESS=peer0.org2.example.com:9051

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

**peer1.org2.example.com:10051**

    # export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer1.org2.example.com/tls/ca.crt

    # export CORE_PEER_ADDRESS=peer1.org2.example.com:10051

    # peer chaincode install -n testcc -v 1.1 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

<br/>

### Instantiate the chaincode (Не заработало)

    # ctrl ^D
    $ docker exec -it cli bash

<br/>

    # export FABRIC_LOGGING_SPEC=info

    # peer chaincode instantiate \
        -o orderer.example.com:7050 \
        --tls true \
        --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem \
        -C mychannel \
        -n testcc \
        -l node \
        -v 1.1 \
        -c '{"Args":["init","a","100","b","200"]}' \
        -P "AND ('Org1MSP.peer','Org2MSP.peer')"

<!--


byfn-sys-channel



-C testchannel \


peer channel create -c mychannel -f ./channel-artifacts/channel.tx --orderer orderer.example.com:7050

    // Думаю должна возвращать OK
    # peer channel list

-->

<br/>

Ошибка!!!

```
Error: error endorsing chaincode: rpc error: code = Unknown desc = access denied: channel [mychannel] creator org [Org1MSP]
```

Смотрю, что в логах контейнера.

```
WARN 037 channel [mychannel]: MSP error: channel doesn't exist
```

<!--

# peer channel join -b ./channel-artifacts/genesis.block
2020-08-20 03:41:13.923 UTC [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
Error: proposal failed (err: bad proposal response 500: "JoinChain" for chainID = byfn-sys-channel failed because of validation of configuration block, because of Invalid configuration block, missing Application configuration group)


-->

<br/>

Потом нужно будет:

**Повторить для:**

    # CORE_PEER_ADDRESS=peer0.org1.example.com:7051

    # CORE_PEER_ADDRESS=peer1.org1.example.com:XXXX

    # CORE_PEER_ADDRESS=peer0.org2.example.com:XXXX

    # CORE_PEER_ADDRESS=peer1.org2.example.com:XXXX

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

The requirements are simple—we need to write a smart contract that will register the property details, change the ownership, query the property details, and execute a few other operations on the properties.

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

Терминал 1:

    $ {
        docker stop $(docker ps -aq)
        docker rm $(docker ps -aq)
        docker system prune -a
    }

    $ cd /home/marley/projects/dev/hyperledger

    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s 1.4.8

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
    $ npm rebuild
    # npm run start -- --peer.address "peer:7052" "--chaincode-id-name" "asset-cc:0.1"

```
Command succeeded

2020-08-20T01:08:46.247Z INFO [lib/handler.js] Successfully registered with peer node. State transferred to "established"
2020-08-20T01:08:46.249Z INFO [lib/handler.js] Successfully established communication with peer node. State transferred to "ready"


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

    $ {
        docker stop $(docker ps -aq)
        docker rm $(docker ps -aq)
        docker system prune -a
    }

    $ cd ~/projects/dev/hyperledger/
    $ rm -rf *

    // Репо ушло вперед. Использую другой вариант. В книге предлагают
    // $ git clone https://github.com/hyperledger/fabric-samples.git

    // It is a one-organization network comprising one peer, one orderer, Fabric CA, CouchDB, and CLI container.
    $ curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh | bash -s 1.4.0

    $ cd fabric-samples

    $ cd chaincode

    $ mkdir asset-registery
    $ cd asset-registery

    $ git clone https://github.com/SateDev/hyperledger_chaincode_asset_registry .

    // Ошибка дальше, если не выполнить. (На моем ПК)
    // "Duplicate identifier 'IteratorResult'"
    $ npm update --save-dev @types/node

<br/>

    $ cd ../../

    $ mkdir startup
    $ cd startup

    $ curl -OL https://raw.githubusercontent.com/SateDev/asset-registry-sdk/master/scripts/startup.sh

<br/>

    $ chmod 777 ./startup.sh
    $ ./startup.sh typescript

<br/>

Хм. Ошибка которая дальше не позволит выполнить все, что происходит в книге именно здесь.

<br/>

```
$ docker ps -a
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS                     PORTS                                        NAMES
f5ceffcc62dd        hyperledger/fabric-peer      "peer node start"        18 seconds ago      Exited (2) 5 seconds ago                                                peer0.org1.example.com
1ee3c124fae2        hyperledger/fabric-orderer   "orderer"                21 seconds ago      Up 19 seconds              0.0.0.0:7050->7050/tcp                       orderer.example.com
c28e2b4b5ff3        hyperledger/fabric-ca        "sh -c 'fabric-ca-se…"   21 seconds ago      Up 18 seconds              0.0.0.0:7054->7054/tcp                       ca.example.com
57addf35f182        hyperledger/fabric-couchdb   "tini -- /docker-ent…"   21 seconds ago      Up 17 seconds              4369/tcp, 9100/tcp, 0.0.0.0:5984->5984/tcp   couchdb
```

Фабрика запустилась.
Но потом упала.

<br/>

### Enrolment and registration of admin and user

using CA server

    $ cd ~/projects/dev/hyperledger/

    $ git clone https://github.com/SateDev/asset-registry-api

    $ cd asset-registry-api

    $ code .

Заменить во всем проекте 137.117.81.211 и 52.187.123.234 на localhost

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

Это из-за того, что исходники для следующей части. Нужно. Чтобы запустить нужно сопоставить коды из проекта с тем, что у индуса на картинках в книге.

Если не хочется разбираться, можно отправиться к следующей главе книги.

    $ cp invoke.js invoke1.js

    $ vi invoke1.js

<br/>

```js
'use strict';

const Fabric_Client = require('fabric-client');
const path = require('path');
const util = require('util');
const os = require('os');

async function invoke() {
  console.log('\n\n --- invoke.js - start');
  try {
    console.log('Setting up client side network objects');
    // fabric client instance
    // starting point for all interactions with the fabric network
    const fabric_client = new Fabric_Client();

    // setup the fabric network
    // -- channel instance to represent the ledger named "mychannel"
    const channel = fabric_client.newChannel('mychannel');
    console.log('Created client side object to represent the channel');
    // -- peer instance to represent a peer on the channel
    const peer = fabric_client.newPeer('grpc://localhost:7051');
    console.log('Created client side object to represent the peer');
    // -- orderer instance to reprsent the channel's orderer
    const orderer = fabric_client.newOrderer('grpc://localhost:7050');
    console.log('Created client side object to represent the orderer');

    // This sample application uses a file based key value stores to hold
    // the user information and credentials. These are the same stores as used
    // by the 'registerUser.js' sample code
    const member_user = null;
    const store_path = path.join(__dirname, 'hfc-key-store');
    console.log('Setting up the user store at path:' + store_path);
    // create the key value store as defined in the fabric-client/config/default.json 'key-value-store' setting
    const state_store = await Fabric_Client.newDefaultKeyValueStore({
      path: store_path,
    });
    // assign the store to the fabric client
    fabric_client.setStateStore(state_store);
    const crypto_suite = Fabric_Client.newCryptoSuite();
    // use the same location for the state store (where the users' certificate are kept)
    // and the crypto store (where the users' keys are kept)
    const crypto_store = Fabric_Client.newCryptoKeyStore({
      path: store_path,
    });
    crypto_suite.setCryptoKeyStore(crypto_store);
    fabric_client.setCryptoSuite(crypto_suite);

    // get the enrolled user from persistence and assign to the client instance
    //    this user will sign all requests for the fabric network
    const user = await fabric_client.getUserContext('user1', true);
    if (user && user.isEnrolled()) {
      console.log('Successfully loaded "user1" from user store');
    } else {
      throw new Error('\n\nFailed to get user1.... run registerUser.js');
    }

    console.log('Successfully setup client side');
    console.log('\n\nStart invoke processing');

    // get a transaction id object based on the current user assigned to fabric client
    // Transaction ID objects contain more then just a transaction ID, also includes
    // a nonce value and if built from the client's admin user.
    const tx_id = fabric_client.newTransactionID();
    console.log(
      util.format('\nCreated a transaction ID: %s', tx_id.getTransactionID())
    );

    const proposal_request = {
      targets: [peer],
      chaincodeId: 'asset',
      fcn: 'createProperty',
      args: ['P100003', 'howbe', '2838', 'somehg', 'asdf', '2323', 'someowner'],
      chainId: 'mychannel',
      txId: tx_id,
    };

    // notice the proposal_request has the peer defined in the 'targets' attribute.
    // Send the transaction proposal to the endorsing peers.
    // The peers will run the function requested with the arguments supplied.
    // based on the current state of the ledger. If the chaincode successfully.
    // runs this simulation it will return a positive result in the endorsement.
    const endorsement_results = await channel.sendTransactionProposal(
      proposal_request
    );

    // The results will contain a few different items
    // first is the actual endorsements by the peers, these will be the responses
    //    from the peers. In our sammple there will only be one results since
    //    only sent the proposal to one peer.
    // second is the proposal that was sent to the peers to be endorsed. This will
    //    be needed later when the endorsements are sent to the orderer.
    // second is the proposal that was sent
    const proposalResponses = endorsement_results[0];
    const proposal = endorsement_results[1];

    // check the results to decide if we should send the endorsment to be orderered
    if (proposalResponses[0] instanceof Error) {
      console.error(
        'Failed to send Proposal. Received an error :: ' +
          proposalResponses[0].toString()
      );
      throw proposalResponses[0];
    } else if (
      proposalResponses[0].response &&
      proposalResponses[0].response.status === 200
    ) {
      console.log(
        util.format(
          'Successfully sent Proposal and received response: Status - %s',
          proposalResponses[0].response.status
        )
      );
    } else {
      const error_message = util.format(
        'Invoke chaincode proposal:: %j',
        proposalResponses[i]
      );
      console.error(error_message);
      throw new Error(error_message);
    }

    // The proposal was good, now send to the orderer to have the transaction
    // committed.

    const commit_request = {
      orderer: orderer,
      proposalResponses: proposalResponses,
      proposal: proposal,
    };

    //Get the transaction ID string to be used by the event processing
    const transaction_id_string = tx_id.getTransactionID();

    // create an array to hold on the asynchronous calls to be executed at the
    // same time
    const promises = [];

    // this will send the proposal to the orderer during the execuction of
    // the promise 'all' call.

    const sendPromise = channel.sendTransaction(commit_request);
    //we want the send transaction first, so that we know where to check status

    promises.push(sendPromise);

    // get an event hub that is associated with our peer
    let event_hub = channel.newChannelEventHub(peer);

    // create the asynchronous work item

    let txPromise = new Promise((resolve, reject) => {
      // setup a timeout of 30 seconds
      // if the transaction does not get committed within the timeout period,
      // report TIMEOUT as the status. This is an application timeout and is a
      // good idea to not let the listener run forever.
      let handle = setTimeout(() => {
        event_hub.unregisterTxEvent(transaction_id_string);
        event_hub.disconnect();
        resolve({ event_status: 'TIMEOUT' });
      }, 30000);

      // this will register a listener with the event hub. THe included callbacks
      // will be called once transaction status is received by the event hub or
      // an error connection arises on the connection.

      event_hub.registerTxEvent(
        transaction_id_string,
        (tx, code) => {
          // this first callback is for transaction event status

          // callback has been called, so we can stop the timer defined above
          clearTimeout(handle);

          // now let the application know what happened
          const return_status = {
            event_status: code,
            tx_id: transaction_id_string,
          };
          if (code !== 'VALID') {
            console.error('The transaction was invalid, code = ' + code);
            resolve(return_status); // we could use reject(new Error('Problem with the tranaction, event status ::'+code));
          } else {
            console.log(
              'The transaction has been committed on peer ' +
                event_hub.getPeerAddr()
            );
            resolve(return_status);
          }
        },
        (err) => {
          //this is the callback if something goes wrong with the event registration or processing
          reject(new Error('There was a problem with the eventhub ::' + err));
        },
        { disconnect: true } //disconnect when complete
      );

      // now that we have a protective timer running and the listener registered,
      // have the event hub instance connect with the peer's event service
      event_hub.connect();
      console.log(
        'Registered transaction listener with the peer event service for transaction ID:' +
          transaction_id_string
      );
    });

    // set the event work with the orderer work so they may be run at the same time
    promises.push(txPromise);

    // now execute both pieces of work and wait for both to complete
    console.log('Sending endorsed transaction to the orderer');
    const results = await Promise.all(promises);

    // since we added the orderer work first, that will be the first result on
    // the list of results
    // success from the orderer only means that it has accepted the transaction
    // you must check the event status or the ledger to if the transaction was
    // committed
    if (results[0].status === 'SUCCESS') {
      console.log('Successfully sent transaction to the orderer');
    } else {
      const message = util.format(
        'Failed to order the transaction. Error code: %s',
        results[0].status
      );
      console.error(message);
      return false;
    }

    if (results[1] instanceof Error) {
      console.error(message);
      return false;
    } else if (results[1].event_status === 'VALID') {
      console.log(
        'Successfully committed the change to the ledger by the peer'
      );
      console.log('\n\n - try running "node query.js" to see the results');
      return true;
    } else {
      const message = util.format(
        'Transaction failed to be committed to the ledger due to : %s',
        results[1].event_status
      );
      console.error(message);
      return false;
    }
  } catch (error) {
    console.log('Unable to invoke ::' + error.toString());
  }
  console.log('\n\n --- invoke.js - end');
}

invoke();
```

<br/>

    $ node invoke1.js

Оказалось, что контейнер peer остановлен.

    $ docker docker ps -a

Поднял его руками.

    $ docker start a2d5c967340a

    $ telnet localhost 7051

OK

<br/>

Всеравно ошибка.

```
Start invoke processing

Created a transaction ID: 6f7760d5fc6824372f4cf7f1d581d18589e872150a0ba2ce6d05989ba31e93f0
2020-08-20T00:00:22.309Z - error: [Peer.js]: sendProposal - timed out after:45000
Failed to send Proposal. Received an error :: Error: REQUEST_TIMEOUT
Unable to invoke ::Error: REQUEST_TIMEOUT

```

    $ docker logs f5ceffcc62dd

```
2020-08-20 00:19:56.664 UTC [couchdb] CreateCouchDatabase -> ERRO 028 Error calling CouchDB CreateDatabaseIfNotExist() for dbName: mychannel_, error: error decoding response body: json: cannot unmarshal string into Go struct field DBInfo.purge_seq of type int
panic: error during commit to txmgr: error decoding response body: json: cannot unmarshal string into Go struct field DBInfo.purge_seq of type int
	panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x28 pc=0xcecbb6]
```

<br/>

Далее нужно подготовить код для query.js

    $ node query.js

<br/>

### Invoking ChangePropertyOwner from Fabric SDK

    $ node changeOwner.js
    $ node query.js

Вернусь и попробую победить, после завершения чтения книги.

<br/>

## Fabric SDK: Building End-to-End Application with Fabric Network

<br/>

    $ cd ~/projects/dev/hyperledger/asset-registry-api

<br/>

В файле routes.js у индуса опечатка.
Нужно, чтобы было

```
var changeOwner = require('./changeOwner');
```

    $ npm start

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

Приложение запустилось.
Но при попытке добавить данные появляется сообщение об ошибке без детализации.
В консолях сообщений об ошибках нет.
Нужно дебажить.

<br/>

## Fabric in Production

Не до production пока
