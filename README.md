# Mesos Debian packaging

Build scripts to create a Mesos Debian package with [FPM](https://github.com/jordansissel/fpm) for simple installation in a cluster. 

Mesos is a cluster manager that provides efficient resource isolation and sharing across distributed applications, or frameworks. It can run Hadoop, MPI, Hypertable, Spark (a new framework for low-latency interactive and iterative jobs), and other applications. Currently is in the Apache Incubator and going through rapid development, though stable enough for a production usage. See [Mesos website](http://incubator.apache.org/mesos/) for more details.

## Packaging requirements
  * ruby
  * prerequisites:

```
    sudo apt-get install ruby ruby-dev python-dev autoconf automake git make libssl-dev libcurl3 libtool
    sudo gem install fpm
```

## Mesos requirements 
(See https://mesos.apache.org/gettingstarted/ for more information)

### Ubuntu 14.04

Following are the instructions for stock Ubuntu 14.04. If you are using a different OS, please install the packages accordingly.

    # Update the packages.
    $ sudo apt-get update

    # Install the latest OpenJDK.
    $ sudo apt-get install -y openjdk-7-jdk

    # Install autotools (Only necessary if building from git repository).
    $ sudo apt-get install -y autoconf libtool

    # Install other Mesos dependencies.
    $ sudo apt-get -y install build-essential python-dev python-boto libcurl4-nss-dev libsasl2-dev maven libapr1-dev libsvn-dev

### Mac OS X Yosemite

Following are the instructions for stock Mac OS X Yosemite. If you are using a different OS, please install the packages accordingly.

    # Install Command Line Tools.
    $ xcode-select --install

    # Install Homebrew.
    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    # Install libraries.
    $ brew install autoconf automake libtool subversion maven

### CentOS 6.6

Following are the instructions for stock CentOS 6.6. If you are using a different OS, please install the packages accordingly.

    # Install a few utility tools
    $ sudo yum install -y tar wget which

    # 'Mesos > 0.21.0' requires a C++ compiler with full C++11 support,
    # (e.g. GCC > 4.8) which is available via 'devtoolset-2'.
    # Fetch the Scientific Linux CERN devtoolset repo file.
    $ sudo wget -O /etc/yum.repos.d/slc6-devtoolset.repo http://linuxsoft.cern.ch/cern/devtoolset/slc6-devtoolset.repo

    # Import the CERN GPG key.
    $ sudo rpm --import http://linuxsoft.cern.ch/cern/centos/7/os/x86_64/RPM-GPG-KEY-cern

    # Fetch the Apache Maven repo file.
    $ sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo

    # 'Mesos > 0.21.0' requires 'subversion > 1.8' devel package, which is
    # not available in the default repositories.
    # Add the WANdisco SVN repo file: '/etc/yum.repos.d/wandisco-svn.repo' with content:

      [WANdiscoSVN]
      name=WANdisco SVN Repo 1.8
      enabled=1
      baseurl=http://opensource.wandisco.com/centos/6/svn-1.8/RPMS/$basearch/
      gpgcheck=1
      gpgkey=http://opensource.wandisco.com/RPM-GPG-KEY-WANdisco

    # Install essential development tools.
    $ sudo yum groupinstall -y "Development Tools"

    # Install 'devtoolset-2-toolchain' which includes GCC 4.8.2 and related packages.
    $ sudo yum install -y devtoolset-2-toolchain

    # Install other Mesos dependencies.
    $ sudo yum install -y apache-maven python-devel java-1.7.0-openjdk-devel zlib-devel libcurl-devel openssl-devel cyrus-sasl-devel cyrus-sasl-md5 apr-devel subversion-devel apr-util-devel

    # Enter a shell with 'devtoolset-2' enabled.
    $ scl enable devtoolset-2 bash
    $ g++ --version  # Make sure you've got GCC > 4.8!

### CentOS 7.1

Following are the instructions for stock CentOS 7.1. If you are using a different OS, please install the packages accordingly.

    # Install a few utility tools
    $ sudo yum install -y tar wget

    # Fetch the Apache Maven repo file.
    $ sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo

    # 'Mesos > 0.21.0' requires 'subversion > 1.8' devel package, which is
    # not available in the default repositories.
    # Add the WANdisco SVN repo file: '/etc/yum.repos.d/wandisco-svn.repo' with content:

      [WANdiscoSVN]
      name=WANdisco SVN Repo 1.9
      enabled=1
      baseurl=http://opensource.wandisco.com/centos/7/svn-1.9/RPMS/$basearch/
      gpgcheck=1
      gpgkey=http://opensource.wandisco.com/RPM-GPG-KEY-WANdisco

    # Install essential development tools.
    $ sudo yum groupinstall -y "Development Tools"

    # Install other Mesos dependencies.
    $ sudo yum install -y apache-maven python-devel java-1.7.0-openjdk-devel zlib-devel libcurl-devel openssl-devel cyrus-sasl-devel cyrus-sasl-md5 apr-devel subversion-devel apr-util-devel
  
  
## Set maintainer

define in e.g. `~/.bash_profile` a `MAINTAINER` variable

	export MAINTAINER="email@example.com"

## Building deb package

	./build_mesos wheezy

## TODO

   * automatic restart of master/slave when upgrading
   * logrotate support
   * service autostart

## Authors

   * Tomas Barton
   * Srdjan Grubor <sgnn7@sgnn7.org>

