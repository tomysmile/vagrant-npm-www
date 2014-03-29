# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Update apt-get once
  $update_apt_get = <<SCRIPT
  if ! test -f .updated_apt_get; then
    sudo apt-get update
    touch .updated_apt_get
  fi
SCRIPT
  config.vm.provision "shell", inline: $update_apt_get

  # https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#ubuntu-mint-elementary-os
  $install_node = <<SCRIPT
  if ! which node &> /dev/null; then
    sudo apt-get install -y python-software-properties python g++ make
    sudo add-apt-repository -y ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install -y nodejs
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_node

  # Install test dependency on `git`
  $install_git = <<SCRIPT
  if ! which git &> /dev/null; then
    sudo apt-get install git -y
  fi
SCRIPT
  config.vm.provision "shell", inline: $install_git

  # Clone `npm-www repository
  $clone_repository = <<SCRIPT
  cd /vagrant
  if ! test -d npm-www &> /dev/null; then
    git clone https://github.com/npm/npm-www.git
  fi
SCRIPT
  config.vm.provision "shell", inline: $clone_repository

  # Notes from before
  # ---------------------
  # ELASTIC SEARCH
  # TODO: This should be in /tmp or /usr/local/lib
  # http://stackoverflow.com/questions/10268583/how-to-automate-download-and-installation-of-java-jdk-on-linux
  # wget http://download.oracle.com/otn-pub/java/jdk/7/jre-7-linux-x64.tar.gz --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"
  # tar xvf jre-7-linux-x64.tar.gz
  # sudo ln -s $PWD/jre1.7.0/bin/java /usr/bin/java

  # wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.7.tar.gz
  # tar xvzf elasticsearch-0.90.7.tar.gz
  # echo "PATH=$PATH:$PWD/elasticsearch-0.90.7/bin" >> /etc/environment

  # COUCH DB
  # TODO: Pray this is a recent version
  # sudo apt-get install couchdb -y

  # REDIS
  # sudo apt-get install redis-server -y
end