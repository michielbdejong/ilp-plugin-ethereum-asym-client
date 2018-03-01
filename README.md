# ILP Plugin Ethereum Asym Client
> Client to Ethereum Asym Server

- [Description](#description)
- [Usage](#usage)

## Description

**This plugin is still under development. Don't use it for large amounts of money.**

This is an implementation of an ILP integration with Ethereum. It uses simple
unidirectional payment channels on Ethereum, by making use of the
[Machinomy](https://github.com/machinomy/machinomy) library.

One party must run an [Ethereum Asym
Server](https://github.com/sharafian/ilp-plugin-ethereum-asym-server) instance,
and then any number of clients can connect by using this Asym Client. Each
client opens a payment channel to the server, and will immediately send a
claim. This claim is to cover the transaction fee of the server opening a
channel to the client. The end result is that the server and client have two
payment channels, allowing either one to send and receive.

Interleger packets are passed over the websocket connection that the client and
server share, and then are periodically settled by passing claims over the
websocket connection. The [ILP
Connector](https://github.com/interledgerjs/ilp-connector) will manage this
logic for you.

Because this plugin allows you to connect to the Interledger, you can use your
Ether to pay anyone else on the network, regardless of what system they choose
to use.

## Usage

You must have a local ethereum provider running in order to use this plugin.
The Machinomy contracts must be deployed on the chain that you connect to.

```js
new PluginEthereumAsymClient({
  account: '0x....', // Your ethereum account
  db: 'machinomy_db', // The db file created by machinomy
  provider: 'http://localhost:8545', // ethereum provider 
  minimumChannelAmount: '10000', // amount with which to fund the channel
})
```

## Connecting to the testnet

Follow the instructions from https://gist.github.com/cryptogoth/10a98e8078cfd69f7ca892ddbdcf26bc
Run:
```sh
npm install
ADDRESS=0xb9458d0076cc76d4568ebaac482ace6f1b30becb node scripts/test.js
```

You will run into https://github.com/sharafian/ilp-plugin-ethereum-asym-client/issues/2, which we're currently fixing!
