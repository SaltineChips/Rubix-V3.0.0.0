RuBiX [RBX] 2017-2019 integration/staging tree
=====================================

http://www.rubixcoin.com

What is the RuBiX [RBX] Blockchain?
-----------------------------------
*TODO: Update documentation regarding implemented tech as this section is out of date and much progress and upgrades have been made to mentioned sections...*

### Overview
Rubix is a blockchain project with the goal of offering secured messaging, masternodes and an overall pleasing experience to the user.

### Blockchain Technology
The RuBiX [RBX] Blockchain is an experimental smart contract platform protocol that enables 
instant payments to anyone, anywhere in the world in a private, secure manner. 
RuBiX [RBX] uses peer-to-peer blockchain technology developed by Bitcoin to operate
with no central authority: managing transactions, execution of contracts, and 
issuing money are carried out collectively by the network. RuBiX [RBX] is the name of 
open source software which enables the use of this protocol.

### Custom Difficulty Retarget Algorithm “VRX”
VRX is designed from the ground up to integrate properly with the Velocity parameter enforcement system to ensure users no longer receive orphan blocks.

### Velocity Block Constraint System
Ensuring Insane stays as secure and robust as possible the CryptoCoderz team have implemented what's known as the Velocity block constraint system. This system acts as third and final check for both mined and peer-accepted blocks ensuring that all parameters are strictly enforced.

Specifications and General info
------------------
RuBiX uses 

		libsecp256k1,
		libgmp,
		Boost1.68,
		OR Boost1.58,  
		Openssl1.02o,
		Berkeley DB 6.2.32,
		QT5.13 to compile


General Specs

		Block Spacing: 5 Minutes
		Stake Minimum Age: 15 Confirmations (PoS-v3) | 30 Minutes (PoS-v2)
		Port: 20029
		RPC Port: 20167


BUILD LINUX
-----------
### Compiling Rubix v2 daemon on Ubunutu 18.04 LTS Xenial
### Note: guide should be compatible with other Ubuntu versions from 14.04+

### Become poweruser
```
sudo -i
```

### Dependencies install
```
sudo apt-get install ntp git build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libqrencode-dev libcurl4-openssl-dev curl libzip-dev; apt-get update; apt-get upgrade; apt-get install git make automake build-essential libboost-all-dev; apt-get install yasm binutils libcurl4-openssl-dev openssl libssl-dev; sudo apt-get install libgmp-dev;
```

### Dependencies build and link
```
cd ~; wget http://download.oracle.com/berkeley-db/db-6.2.32.NC.tar.gz; tar zxf db-6.2.32.NC.tar.gz; cd db-6.2.32.NC/build_unix; ../dist/configure --enable-cxx; make; sudo make install; sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb-6.2.so /usr/lib/libdb-6.2.so; sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb_cxx-6.2.so /usr/lib/libdb_cxx-6.2.so; export BDB_INCLUDE_PATH="/usr/local/BerkeleyDB.6.2/include"; export BDB_LIB_PATH="/usr/local/BerkeleyDB.6.2/lib"
```

### Personal upload EXAMPLE
```
sudo cp -r /home/ftpuser/ftp/files/RBX-clean/. ~/Rubix
```

### GitHub pull RECOMMENDED
```
cd ~; git clone https://github.com/SaltineChips/Rubix
```

### Build Rubix daemon
```
cd ~/Rubix/src; chmod a+x obj; chmod a+x leveldb/build_detect_platform; chmod a+x secp256k1; chmod a+x leveldb; chmod a+x ~/Rubix/src; chmod a+x ~/Rubix; make -f makefile.unix USE_UPNP=-; cd ~; cp -r ~/Rubix/src/RuBiXd /usr/local/bin/RuBiXd;
```

### Create config file for daemon
```
sudo ufw allow 20029/tcp; sudo ufw allow 20167/tcp; sudo ufw allow 27017/tcp; sudo mkdir ~/.RBX; cat << "CONFIG" >> ~/.RBX/RuBiX.conf
listen=1
server=1
daemon=1
testnet=0
rpcuser=rubixuser
rpcpassword=SomeCrazyPasswordGoesHere
rpcport=20167
port=20029
rpcconnect=127.0.0.1
rpcallowip=127.0.0.1
addnode=46.101.73.64
addnode=188.166.109.87
addnode=159.203.240.221
addnode=165.227.34.98
CONFIG
chmod 700 ~/.RBX/RuBiX.conf; chmod 700 ~/.RBX; ls -la ~/.RBX
```

### Run Rubix daemon
```
cd ~; RuBiXd; RuBiXd getinfo
```

### Troubleshooting
### for basic troubleshooting run the following commands when compiling:
### this is for minupnpc errors compiling

```
make clean -f makefile.unix USE_UPNP=-
make -f makefile.unix USE_UPNP=-
```

License
-------

RuBiX [RBX] is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/CryptoCoderz/RBX/tags) are created
regularly to indicate new official, stable release versions of RuBiX [RBX].

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).

The developer [mailing list](https://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev)
should be used to discuss complicated or controversial changes before working
on a patch set.

Developer Slack can be found at http://rubixcointeam.slack.com. (this is abandoned)

Developer Discord can be found at https://discord.gg/rg9PfAR. (this is active)

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](/doc/unit-tests.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.
