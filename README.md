# Apache Mesos Packaging

Build scripts to create Apache Mesos packages with [FPM](https://github.com/jordansissel/fpm) for simple installation in a cluster.

Apache Mesos is a cluster manager that provides efficient resource isolation and sharing across distributed applications, or frameworks. It can run Hadoop, MPI, Hypertable, Spark (a new framework for low-latency interactive and iterative jobs), and other applications. Currently is in the Apache Incubator and going through rapid development, though stable enough for a production usage. See [Mesos website](http://incubator.apache.org/mesos/) for more details.

## Packaging Requirements

# Debian 9 and Ubuntu 14
```bash
sudo apt-get install ruby ruby-dev python-dev autoconf automake default-jdk dpkg-dev git make \
  libssl-dev libcurl3 libtool libapr1 libapr1-dev libcurl3 libcurl4-openssl-dev maven libsasl2-2 \
  libsasl2-dev libsvn-dev zlib1g-dev libevent-dev
sudo gem install fpm
```

# Debian 10 and Ubuntu 18
```bash
sudo apt-get install autoconf automake default-jdk dpkg-dev git libapr1 libapr1-dev libboost-all-dev \
  libcurl4 libcurl4-openssl-dev libsasl2-2 libsasl2-dev libssl-dev libsvn-dev libtool make maven \
  python-dev ruby ruby-dev zlib1g-dev libevent-dev
sudo gem install fpm
```

## Mesos Requirements

Mesos has its own OS-level build requirements that need to be installed as well before building.

See [getting-started](https://mesos.apache.org/getting-started/) for more information.


## Setting the Maintainer

define in e.g. `~/.bash_profile` a `MAINTAINER` variable

```bash
export MAINTAINER="email@example.com"
```

## Setting `make` Options (optional)

```bash
export MAKEFLAGS=-j8
```

## Building deb or rpm Package

```bash
./build_mesos
```

## TODO

   * automatic restart of master/slave when upgrading
   * logrotate support
   * service autostart

## Authors

   * Tomas Barton
   * Srdjan Grubor <sgnn7@sgnn7.org>
