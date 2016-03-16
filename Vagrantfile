# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.define "zatan-vm" do |vm_define|
  end

  config.vm.hostname = "zatan.local"

  config.vm.network "forwarded_port", guest: 8000, host: 8010

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.name = "zatan-vm"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git build-essential python python-dev python-virtualenv postgresql postgresql-server-dev-all postgis postgresql-9.3-postgis-2.1 rabbitmq-server libevent-dev
    sudo -u postgres psql --command="CREATE USER tracker_project WITH PASSWORD 'tracker_project';"
    sudo -u postgres psql --command="CREATE DATABASE tracker_project WITH OWNER tracker_project;"
    sudo -u postgres psql --command="GRANT ALL PRIVILEGES ON DATABASE tracker_project TO tracker_project;"
    sudo -u postgres psql --command="CREATE EXTENSION postgis; CREATE EXTENSION postgis_topology;" tracker_project
  SHELL
end
