# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vagrant.plugins = "vagrant-hostsupdater"
  config.hostsupdater.aliases = ["hello.com", "python.com"]

  # config.vm.network "public_network"


  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
    cp -rf /vagrant/www/* /var/www
    cp -rf /vagrant/sites-available/* /etc/apache2/sites-available
    a2enmod ssl
    a2enmod cgid
    chmod +x ../../var/www/python/main.py
    a2ensite hello
    service apache2 restart
  SHELL
end
