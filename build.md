# Build in Ubuntu

- Required

```
apt-get install libc6-dev libssl-dev openssl lua5.1 liblua5.1-dev libz-dev -y
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
