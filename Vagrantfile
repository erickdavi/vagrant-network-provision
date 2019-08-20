# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  #Configuracao da VM1
  config.vm.define "vm1" do |vm1|
    vm1.vm.provider "virtualbox" do |vb|
      vb.name = "vm1"
      vb.memory = "1024"
      #vb.cpus = 2
    end  
    vm1.vm.network "forwarded_port", guest: 80, host: 80
    vm1.vm.network "private_network", ip: "10.0.0.1"
    #vm1.vm.network "public_network", ip: "192.168.0.250"
    vm1.vm.synced_folder "vm1/", "/home/vagrant/vm1" 

    vm1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get upgrade -y
      apt-get install -y apache2
    SHELL


  end

  #Configuracao da VM2
  config.vm.define "vm2" do |vm2|
    vm2.vm.provider "virtualbox" do |vb|
      vb.name = "vm2"
      vb.memory = "1024"
      #vb.cpus = 2
    end
    vm2.vm.network "private_network", ip: "10.0.0.2"
    #vm2.vm.network "public_network", ip: "192.168.0.251"
    vm2.vm.synced_folder "vm2/", "/home/vagrant/vm2"
    
    vm2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get upgrade -y
      sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password 123456'
      sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password 123456'
      sudo apt-get -y install mysql-server      
    SHELL
  
  end
end
