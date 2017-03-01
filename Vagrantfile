# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "bento/ubuntu-14.04"

  config.vm.provider "virtualbox" do |vb|
    vb.cpus = "2"
    vb.memory = "4096"
  end

  config.vm.provider "vmware_fusion" do |v|
    v.vmx["memsize"] = "4096"
    v.vmx["numvcpus"] = "2"
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo "*** updating apt cache ***"
    sudo apt-get -y -qq update
    echo "*** installing prereqs ***"
    sudo apt-get install -y -qq ruby ruby-dev autoconf build-essential \
      python-dev python-boto libcurl3 libcurl4-nss-dev libsasl2-dev \
      maven libapr1-dev libsvn-dev make libssl-dev libtool \
      openjdk-7-jdk
    echo "*** installing fpm ***"
    sudo gem install fpm
  SHELL
end
