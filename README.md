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

UNIX BUILD NOTES
================

To Build
--------
```
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt install -y build-essential libssl1.0.0 libdb++-dev libboost-all-dev miniupnpc libqrencode-dev git libssl-dev libminiupnpc-dev
git clone https://github.com/Gr1dd/CompCoin.git
cd CompCoin
cd src
make -f makefile.unix            # Headless CompCoin
```
See readme-qt.rst for instructions on building CompCoin QT,
the graphical CompCoin.

Dependencies
------------

 Library     Purpose           Description
----------------------------------------------

1. libssl1.0-dev     SSL Support       Secure communications
2. libdb       Berkeley DB       Blockchain & wallet storage
3. libboost    Boost             C++ Library
4. miniupnpc   UPnP Support      Optional firewall-jumping support
5. libqrencode QRCode generation Optional QRCode generation


#### To build with PIE, use:
###### ```make -f makefile.unix ... -e PIE=1```


Troubleshooting
---------------

Error:
g++: error: {path-to-nlc-source}/src/leveldb/libleveldb.a: No such file or directory
g++: error: {path-to-nlc-source}/src/leveldb/libmemenv.a: No such file or directory

Solution:
$ cd leveldb
$ chmod 755 build_detect_platform
