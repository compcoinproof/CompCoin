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
sudo ./CompCoind -conf=$PWD/test.conf -seednode=fleabags.net -addnode=fleabags.net -dns -debug -debugnet -dnsseed -upnp
```

Default username is: CompCoinrpc

Default address is: http://YOURIPADDRESS:2667

To get password:

```
docker exec CONTAINERNAME echo $PASS
```

OR IF NOT IN DOCKER!

```
echo $PASS
```
And you're good to go!

See readme-qt.rst for instructions on building CompCoin QT,
the graphical CompCoin.

#### To build with PIE, use:
###### ```make -f makefile.unix ... -e PIE=1```


Making RPC transfers and command-line options for the DMG, EXE and DOCKER executable!!! SEE BELOW
------------------------------------------
```
Options:
  -?                     This help message
  -conf=<file>           Specify configuration file (default: CompCoin.conf)
  -pid=<file>            Specify pid file (default: CompCoind.pid)
  -datadir=<dir>         Specify data directory
  -wallet=<dir>          Specify wallet file (within data directory)
  -dbcache=<n>           Set database cache size in megabytes (default: 25)
  -dblogsize=<n>         Set database disk log size in megabytes (default: 100)
  -timeout=<n>           Specify connection timeout in milliseconds (default: 5000)
  -proxy=<ip:port>       Connect through socks proxy
  -socks=<n>             Select the version of socks proxy to use (4-5, default: 5)
  -tor=<ip:port>         Use proxy to reach tor hidden services (default: same as -proxy)
  -dns                   Allow DNS lookups for -addnode, -seednode and -connect
  -port=<port>           Listen for connections on <port> (default: 2668 or testnet: 12668)
  -maxconnections=<n>    Maintain at most <n> connections to peers (default: 125)
  -addnode=<ip>          Add a node to connect to and attempt to keep the connection open
  -connect=<ip>          Connect only to the specified node(s)
  -seednode=<ip>         Connect to a node to retrieve peer addresses, and disconnect
  -externalip=<ip>       Specify your own public address
  -onlynet=<net>         Only connect to nodes in network <net> (IPv4, IPv6 or Tor)
  -discover              Discover own IP address (default: 1 when listening and no -externalip)
  -irc                   Find peers using internet relay chat (default: 0)
  -listen                Accept connections from outside (default: 1 if no -proxy or -connect)
  -bind=<addr>           Bind to given address. Use [host]:port notation for IPv6
  -dnsseed               Find peers using DNS lookup (default: 1)
  -staking               Stake your coins to support network and gain reward (default: 1)
  -synctime              Sync time with other nodes. Disable if time on your system is precise e.g. syncing with NTP (default: 1)
  -cppolicy              Sync checkpoints policy (default: strict)
  -banscore=<n>          Threshold for disconnecting misbehaving peers (default: 100)
  -bantime=<n>           Number of seconds to keep misbehaving peers from reconnecting (default: 86400)
  -maxreceivebuffer=<n>  Maximum per-connection receive buffer, <n>*1000 bytes (default: 5000)
  -maxsendbuffer=<n>     Maximum per-connection send buffer, <n>*1000 bytes (default: 1000)
  -detachdb              Detach block and address databases. Increases shutdown time (default: 0)
  -paytxfee=<amt>        Fee per KB to add to transactions you send
  -mininput=<amt>        When creating transactions, ignore inputs with value less than this (default: 0.01)
  -server                Accept command line and JSON-RPC commands
  -testnet               Use the test network
  -debug                 Output extra debugging information. Implies all other -debug* options
  -debugnet              Output extra network debugging information
  -logtimestamps         Prepend debug output with timestamp
  -shrinkdebugfile       Shrink debug.log file on client startup (default: 1 when no -debug)
  -printtoconsole        Send trace/debug info to console instead of debug.log file
  -printtodebugger       Send trace/debug info to debugger
  -rpcuser=<user>        Username for JSON-RPC connections
  -rpcpassword=<pw>      Password for JSON-RPC connections
  -rpcport=<port>        Listen for JSON-RPC connections on <port> (default: 2667 or testnet: 12667)
  -rpcallowip=<ip>       Allow JSON-RPC connections from specified IP address
  -rpcconnect=<ip>       Send commands to node running on <ip> (default: 127.0.0.1)
  -blocknotify=<cmd>     Execute command when the best block changes (%s in cmd is replaced by block hash)
  -walletnotify=<cmd>    Execute command when a wallet transaction changes (%s in cmd is replaced by TxID)
  -confchange            Require a confirmations for change (default: 0)
  -enforcecanonical      Enforce transaction scripts to use canonical PUSH operators (default: 1)
  -alertnotify=<cmd>     Execute command when a relevant alert is received (%s in cmd is replaced by message)
  -upgradewallet         Upgrade wallet to latest format
  -keypool=<n>           Set key pool size to <n> (default: 100)
  -rescan                Rescan the block chain for missing wallet transactions
  -salvagewallet         Attempt to recover private keys from a corrupt wallet.dat
  -checkblocks=<n>       How many blocks to check at startup (default: 2500, 0 = all)
  -checklevel=<n>        How thorough the block verification is (0-6, default: 1)
  -loadblock=<file>      Imports blocks from external blk000?.dat file

Block creation options:
  -blockminsize=<n>      Set minimum block size in bytes (default: 0)
  -blockmaxsize=<n>      Set maximum block size in bytes (default: 250000)
  -blockprioritysize=<n> Set maximum size of high-priority/low-fee transactions in bytes (default: 27000)

SSL options: (see the Bitcoin Wiki for SSL setup instructions)
  -rpcssl                                  Use OpenSSL (https) for JSON-RPC connections
  -rpcsslcertificatechainfile=<file.cert>  Server certificate file (default: server.cert)
  -rpcsslprivatekeyfile=<file.pem>         Server private key (default: server.pem)
  -rpcsslciphers=<ciphers>                 Acceptable ciphers (default: TLSv1+HIGH:!SSLv2:!aNULL:!eNULL:!AH:!3DES:@STRENGTH)

UI options:
  -lang=<lang>           Set language, for example "de_DE" (default: system locale)
  -min                   Start minimized
  -splash                Show splash screen on startup (default: 1)
```
