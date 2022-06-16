# iroha-demo

## Overview of Iroha

Hyperledger Iroha is a general purpose permissioned blockchain system that can be used to manage digital assets, identity, and serialized data. This can be useful for applications such as interbank settlement, central bank digital currencies, payment systems, national IDs, and logistics, among others.

## Key features of Iroha
- Simple deployment and maintenance
- Variety of libraries for developers
- Role-based access control
- Modular design, driven by command–query separation principle
- Assets and identity management

## How is it different from Bitcoin or Ethereum?
Bitcoin and Ethereum are designed to be permissionless ledgers where anyone can join and access all the data.

Iroha system interaction is permissioned, meaning that only people with requisite access can interact with the system. Hence, access to all the data can be controlled.

One major difference from Ethereum, in particular, is that Hyperledger Iroha allows users to perform common functions, such as creating and transferring digital assets, by using prebuilt commands that are in the system.

## Iroha terminology

### Account

An Iroha entity that is able to perform specified set of actions. Each account belongs to one of existing domains. An account has some number of roles (can be null).

### Asset

Any countable commodity or value. Each asset is related to one of existing domains. For example, an asset can represent any kind of such units - currency unit, a bar of gold, real estate unit, etc.

### Block

Transaction data is permanently recorded in files called blocks. Blocks are organized into a linear sequence over time (also known as the block chain).

Blocks are signed with the cryptographic signatures of Iroha peers, voting for this block during consensus. Signable content is called payload, so the structure of a block looks like this:


![blocks](images/block.png)

`Outside payload`

- signatures — signatures of peers, which voted for the block during consensus round

`Inside payload`

- height — a number of blocks in the chain up to the block
- timestamp — Unix time (in milliseconds) of block forming by a peer
- array of transactions, which successfully passed validation and consensus step
- hash of a previous block in the chain
- rejected transactions hashes — array of transaction hashes, which did not pass stateful validation step; this field is optional


### Command

A command is an intention to change the state of the network. For example, in order to create a new role in Iroha you have to issue Create role command.

### Consensus

An algorithm to achieve agreement on a block among peers in the network. By having it in the system, reliability is increased.

### Domain

A named abstraction for grouping accounts and assets. For example, it can represent an organisation in the group of organisations working with Iroha.

### Peer

A node that is a part of Iroha network. It participates in consensus process.

### Permission

A named rule that gives the privilege to perform a command.

### Proposal

A set of transactions that have passed only stateless validation.

### Verified Proposal

A set of transactions that have passed both stateless and stateful validation, but were not committed yet.

### Query

A request to Iroha that does not change the state of the network. By performing a query, a client can request data from the state, for example a balance of his account, a history of transactions, etc.

### Quorum

In the context of transactions signing, quorum number is a minimum amount of signatures required to consider a transaction signed. The default value is 1.

### Role

A named abstraction that holds a set of permissions.

### Signatory

Represents an entity that can confirm multisignature transactions for an account. It can be attached to account via AddSignatory and detached via RemoveSignatory.

### Transaction

An ordered set of commands, which is applied to the ledger. Any non-valid command within a transaction leads to rejection of the whole transaction during the validation process.


## What’s inside Iroha?

HL Iroha network consists of several essential components that provide the communication between the nodes. 

![pipeline-diagram](images/pipeline-diagram.png)


### Demo

```sh
$ cd iroha
$ docker-compose up -d
```

`use iroha-cli to test commands (add asset, transfer asset, and query)`

```sh
$ docker exec -it <container name/id> /bin/bash
```

```sh
iroha-cli --account_name root@jtrb
```

<!-- ./iroha-cli --account_name newuser@test --new_account -->

<!-- https://github.com/hyperledger/iroha/blob/main/example/genesis.block -->