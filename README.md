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

cd src/
make -f makefile.unix            # Headless CompCoin

See readme-qt.rst for instructions on building CompCoin QT,
the graphical CompCoin.

Dependencies
------------

 Library     Purpose           Description
 -------     -------           -----------
 libssl1.0-dev     SSL Support       Secure communications
 libdb       Berkeley DB       Blockchain & wallet storage
 libboost    Boost             C++ Library
 miniupnpc   UPnP Support      Optional firewall-jumping support
 libqrencode QRCode generation Optional QRCode generation

Note that libexecinfo should be installed, if you building under *BSD systems. 
This library provides backtrace facility.

miniupnpc may be used for UPnP port mapping.  It can be downloaded from
http://miniupnp.tuxfamily.org/files/.  UPnP support is compiled in and
turned off by default.  Set USE_UPNP to a different value to control this:
 USE_UPNP=-    No UPnP support - miniupnp not required
 USE_UPNP=0    (the default) UPnP support turned off by default at runtime
 USE_UPNP=1    UPnP support turned on by default at runtime

libqrencode may be used for QRCode image generation. It can be downloaded
from http://fukuchi.org/works/qrencode/index.html.en, or installed via
your package manager. Set USE_QRCODE to control this:
 USE_QRCODE=0   (the default) No QRCode support - libqrcode not required
 USE_QRCODE=1   QRCode support enabled

Licenses of statically linked libraries:
 Berkeley DB   New BSD license with additional requirement that linked
               software must be free open source
 Boost         MIT-like license
 miniupnpc     New (3-clause) BSD license

Versions used in this release:
 GCC           4.9.0
 OpenSSL       1.0.1g
 Berkeley DB   5.3.28.NC
 Boost         1.55.0
 miniupnpc     1.9.20140401

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
sudo apt-get install build-essential libssl-dev libdb++-dev libboost-all-dev libqrencode-dev

If using Boost 1.37, append -mt to the boost libraries in the makefile.


Dependency Build Instructions: Gentoo
-------------------------------------

emerge -av1 --noreplace boost openssl sys-libs/db

Take the following steps to build (no UPnP support):
 cd ${CompCoin_DIR}/src
 make -f makefile.unix USE_UPNP=
 strip CompCoind


Notes
-----
The release is built with GCC and then "strip CompCoind" to strip the debug
symbols, which reduces the executable size by about 90%.


miniupnpc
---------
tar -xzvf miniupnpc-1.6.tar.gz
cd miniupnpc-1.6
make
sudo su
make install


Berkeley DB
-----------
You need Berkeley DB. If you have to build Berkeley DB yourself:
../dist/configure --enable-cxx
make


Boost
-----
If you need to build Boost yourself:
sudo su
./bootstrap.sh
./bjam install


Security
--------
To help make your CompCoin installation more secure by making certain attacks impossible to
exploit even if a vulnerability is found, you can take the following measures:

* Position Independent Executable
    Build position independent code to take advantage of Address Space Layout Randomization
    offered by some kernels. An attacker who is able to cause execution of code at an arbitrary
    memory location is thwarted if he doesn't know where anything useful is located.
    The stack and heap are randomly located by default but this allows the code section to be
    randomly located as well.

    On an Amd64 processor where a library was not compiled with -fPIC, this will cause an error
    such as: "relocation R_X86_64_32 against `......' can not be used when making a shared object;"

    To build with PIE, use:
    make -f makefile.unix ... -e PIE=1

    To test that you have built PIE executable, install scanelf, part of paxutils, and use:
    scanelf -e ./CompCoin

    The output should contain:
     TYPE
    ET_DYN

* Non-executable Stack
    If the stack is executable then trivial stack based buffer overflow exploits are possible if
    vulnerable buffers are found. By default, CompCoin should be built with a non-executable stack
    but if one of the libraries it uses asks for an executable stack or someone makes a mistake
    and uses a compiler extension which requires an executable stack, it will silently build an
    executable without the non-executable stack protection.

    To verify that the stack is non-executable after compiling use:
    scanelf -e ./CompCoin

    the output should contain:
    STK/REL/PTL
    RW- R-- RW-

    The STK RW- means that the stack is readable and writeable but not executable.


Troubleshooting
---------------

Error:
g++: error: {path-to-nlc-source}/src/leveldb/libleveldb.a: No such file or directory
g++: error: {path-to-nlc-source}/src/leveldb/libmemenv.a: No such file or directory

Solution:
$ cd leveldb
$ chmod 755 build_detect_platform


Static Build
-------------

1. Build Qt from source (successfully built qt-5.3.2 on Ubuntu 14.04)
    $ ./configure -confirm-license -static -release -opensource -openssl-linked -system-sqlite -no-rpath -nomake tests -no-openssl -no-dbus -nomake examples -qt-xcb -skip qtwebkit -no-icu
    $ make -j 4
    $ make -j 4 install    

2. Set path to new qt built in terminal and make CompCoin-qt
    $ PATH=~/Qt/qt-src-5.3.2/qtbase/bin/:$PATH
    $ qmake USE_DBUS=0 RELEASE=1
    $ make -j 4

Static Build References
-----------------------

Building Qt 5 from Git
https://wiki.qt.io/Building_Qt_5_from_Git

Qt for X11 Requirements
http://doc.qt.io/qt-5/linux-requirement
