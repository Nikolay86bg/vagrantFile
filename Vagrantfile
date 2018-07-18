# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Box Settings
  config.vm.box = "ubuntu/xenial64"

  # Provider Settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  # Network Settings
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  # Folder Settings
  config.vm.synced_folder "../aqualife", "/var/www/html/", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

  # Provision Settings
  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y git
    apt install -y apache2
    a2enmod rewrite
    apt-add-repository ppa:ondrej/php
    apt update
    apt install -y php7.2
    apt install -y libapache2-mod-php7.2
    service apache2 restart
    apt install -y php7.2-common
    apt install -y php7.2-mcrypt
    apt install -y php7.2-zip
    debconf-set-selections <<< 'mysql-server mysql-server/root_password root'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again root'
    apt install -y mysql-server
    apt install -y php7.2-mysql
    apt install -y php-xml
    service apache2 restart
  SHELL
end
