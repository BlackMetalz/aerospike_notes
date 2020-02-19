# Build in Ubuntu

- Required

```
apt-get install libc6-dev libssl-dev openssl lua5.1 liblua5.1-dev libz-dev autoconf -y
```

- Installing libevent
```
wget "https://github.com/libevent/libevent/releases/download/release-2.1.11-stable/libevent-2.1.11-stable.tar.gz"
tar xvf libevent-2.1.11-stable.tar.gz
cd libevent-2.1.11-stable
./configure
make
make install
```

- Clone the source

```
git clone https://github.com/aerospike/aerospike-server.git
```

After the initial cloning of the aerospike-server repo., the submodules must be fetched for the first time using the following command:
```
$ git submodule update --init
```

Build with -j option
```
make -j8 # 8 is number of your core for parallel job
```

Credit: https://github.com/aerospike/aerospike-server
