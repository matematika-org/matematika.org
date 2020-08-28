---
layout: page
title: Hyperleger Fabric - Creating a channel
description: Hyperleger Fabric - Creating a channel
keywords: Blockchain, Hyperleger, Fabric, Официальная документация, Creating a channel
permalink: /blockchain/hyperledger/fabric/official-docs/tutorials/creating-a-channel/
---

# 7.7 Creating a channel

Делаю:

28.08.2020

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

In order to create and transfer assets on a Hyperledger Fabric network, an organization needs to join a channel. Channels are a private layer of communication between specific organizations and are invisible to other members of the network. Each channel consists of a separate ledger that can only be read and written to by channel members, who are allowed to join their peers to the channel and receive new blocks of transactions from the ordering service. While the peers, nodes, and Certificate Authorities form the physical infrastructure of the network, channels are the process by which organizations connect with each other and interact.

<br/>

### Setting up the configtxgen tool

Channels are created by building a channel creation transaction and submitting the transaction to the ordering service. The channel creation transaction specifies the initial configuration of the channel and is used by the ordering service to write the channel genesis block. While it is possible to build the channel creation transaction file manually, it is easier to use the configtxgen tool. The tool works by reading a configtx.yaml file that defines the configuration of your channel, and then writing the relevant information into the channel creation transaction. Before we discuss the configtx.yaml file in the next section, we can get started by downloading and setting up the configtxgen tool.

    $ cd fabric-samples/test-network
    $ export PATH=${PWD}/../bin:$PATH
    $ export FABRIC_CFG_PATH=${PWD}/configtx

<br/>

### Start the network

    $ ./network.sh down && ./network.sh up

Our instance of the test network was deployed without creating an application channel.

<br/>

### Creating an application channel

    $ configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel1.tx -channelID channel1

<br/>

    $ export FABRIC_CFG_PATH=$PWD/../config/

<br/>

    $ {
        export CORE_PEER_TLS_ENABLED=true
        export CORE_PEER_LOCALMSPID="Org1MSP"
        export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
        export CORE_PEER_MSPCONFIGPATH=\${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
        export CORE_PEER_ADDRESS=localhost:7051
    }

<br/>

    // create the channel
    $ peer channel create \
    -o localhost:7050  \
    --ordererTLSHostnameOverride orderer.example.com \
    -c channel1 \
    -f ./channel-artifacts/channel1.tx \
    --outputBlock ./channel-artifacts/channel1.block \
    --tls \
    --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem

<br/>

### Join peers to the channel

