# Mesos Debian packaging

Build scripts to create a Mesos Debian package with [FPM](https://github.com/jordansissel/fpm) for simple installation in a cluster.

Mesos is a cluster manager that provides efficient resource isolation and sharing across distributed applications, or frameworks. It can run Hadoop, MPI, Hypertable, Spark (a new framework for low-latency interactive and iterative jobs), and other applications. Currently is in the Apache Incubator and going through rapid development, though stable enough for a production usage. See [Mesos website](http://incubator.apache.org/mesos/) for more details.

## Packaging requirements

```
    sudo apt-get install ruby ruby-dev python-dev autoconf automake git make libssl-dev libcurl3 \ 
    	libtool build-essential
    sudo gem install fpm
```

## Mesos requirements

Mesos has its own OS-level build requirements that need to be installed as well before building.

See https://mesos.apache.org/gettingstarted/ for more information

## Setting the maintainer

define in e.g. `~/.bash_profile` a `MAINTAINER` variable

	export MAINTAINER="email@example.com"

## Setting make options (optional)

	export MAKEFLAGS=-j8

## Building deb or rpm package

	./build_mesos

## TODO

   * automatic restart of master/slave when upgrading
   * logrotate support
   * service autostart

## Authors

   * Tomas Barton
   * Srdjan Grubor <sgnn7@sgnn7.org>

