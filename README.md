CompCoin (CMP)
===================
Distributed under the MIT/X11 software license.

Copyright © 2009-2017 The Bitcoin developers
Copyright © 2009-2017 The Peercoin developers
Copyright © 2017 The CompCoin developers


-----

Access your wallet at 

http://YOURIP:2667

OR

Connect with the releases.

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
rpcuser=CompCoinrpc
rpcpassword=ISRANDOMLYGENERATED
rpcallowip=*.*.*.*
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
sudo apt install -y build-essential libssl1.0.0 libdb++-dev libboost-all-dev miniupnpc libqrencode-dev git libssl-dev libminiupnpc-dev libleveldb-dev 
git clone https://github.com/Gr1dd/CompCoin.git
cd CompCoin
cd src
cd leveldb
make
cd ..
sudo chmod 777 leveldb/ -R
make -f makefile.unix
export PASS=rpcpassword=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1) 
echo $PASS | sudo tee --append test.conf
sudo chmod 700 test.conf
sudo ./CompCoind --conf=$PWD/test.conf
```

Default username is: CompCoinrpc
Default address is: http://YOURIPADDRESS:2667

To get password:

```
docker exec CONTAINERNAME echo $PASS
```
OR IF NOT IN DOCKER!
echo $PASS

And you're good to go!

See readme-qt.rst for instructions on building CompCoin QT,
the graphical CompCoin.

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
