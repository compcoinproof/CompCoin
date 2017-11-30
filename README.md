CompCoin (CMP)
===================
Distributed under the MIT/X11 software license.

Copyright © 2009-2017 The Bitcoin developers
Copyright © 2009-2017 The Peercoin developers
Copyright © 2017 The CompCoin developers


-----

```
Algorithm: Proof of Stake
Block Time: 1 Minute
Coinbase Maturity: 100 blocks
PoS APR: 8.33%
Minimum Stake Age: 4 hours
rpc port: 2667
p2p port: 2668
testnet rpc: 12667  
testnet p2p port: 12668
PUBKEY_ADDRESS = 28
SCRIPT_ADDRESS = 85
PUBKEY_ADDRESS_TEST = 121
SCRIPT_ADDRESS_TEST = 126
```

CompCoin.conf

```
rpcuser=
rpcpassword=
rpcallowip=127.0.0.1
listen=1
server=1
maxconnections=256
```

```
To compile for Linux:

sudo add-apt-repository ppa:bitcoin/bitcoin

sudo apt-get update

sudo apt-get install libdb-dev libdb++-dev build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git libboost-all-dev libminiupnpc-dev libqt5gui5 libqt5core5a libqt5webkit5-dev libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler libqrencode-dev
 
git clone https://github.com/compcoinproof/CompCoin && cd CompCoin && ./autogen.sh && ./configure && make
```
