# EOTCoin
What is EOT? - Get more information here: 
https://bit-media.org/news/what-is-eot/

Join the encryption of things community here:
http://encryptionofthings.org

## EOTCoin Node Source Code

### Guide: Compiling EOTCoin daemon in Ubuntu Linux

This guide will assist you in compiling a headless client (the daemon) for EOTCoin in Ubuntu Linux. This is a necessary step if you wish to set up a node for EOTCoin. It is assumed that you are starting on a fresh Ubuntu (14.04 x64) installation.

You will need a server with at least 512MB of RAM and 20GB Hard Drive. 

### Set up a swapfile if your system has less than 1.5GB of memory:

    fallocate -l 2G /swapfile
    chown root:root /swapfile
    chmod 0600 /swapfile
    mkswap /swapfile
    swapon /swapfile

If fallocate doesn’t work, you can use
     dd if=/dev/zero of=/swapfile bs=1024 count=1024288
instead.

Initialize swapfile automatically on boot

    nano /etc/fstab
Add this at the bottom: /swapfile none swap sw 0 0

### Install all required dependencies:

    apt-get update && apt-get upgrade
    apt-get install ntp unzip git build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude && aptitude install miniupnpc libminiupnpc-dev

### Pull the source code from github, or upload it yourself:
    git clone https://github.com/EmbeddedDownloads/EOTCoin.git

### compile leveldb:
    cd /EOTCoin/src/leveldb
    chmod +x build_detect_platform
    make clean
    make libleveldb.a libmemenv.a

### Return to source directory, and compile the daemon:

    cd /EOTCoin/src
    make -f makefile.unix

### Strip the file to make it smaller, then relocate it:

    strip EOTCoind
    cp EOTCoind /usr/bin

### Now run the daemon:

    EOTCoind

It will return an error, telling you to set up config file in a directory. Now we’ll set up the config file. Note that this is case sensitive.

    nano ~/.EOTCOIN/EOTCOIN.conf

Add the following, save and exit:

    daemon=1
    server=1
    rpcuser=(username)
    rpcpassword=(strong password)

Run EOTCoind once more and if you did everything correctly, your daemon is now online! Type EOTCoind help for a full list of commands available. 

### To help our developers code faster, please buy them some coffee:
    EOT Wallet: EXuU6PAJxD5qmVYAhYkusLZcgZ36T1aNJP
    BTC Wallet: 13v41hEUHrxfpM3L7kqvLNnaxvsgMqnXL2
