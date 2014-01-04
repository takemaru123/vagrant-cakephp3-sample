# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "CentOS_6.5_x86_64"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.1/centos65-x86_64-20131205.box"
  
  config.vm.network :private_network, ip: "192.168.33.10"

  # cakephpを使うために必要
  config.vm.synced_folder "./", "/vagrant", mount_options: ['dmode=777', 'fmode=666']

  config.omnibus.chef_version = :latest

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "./site-cookbooks"
    chef.add_recipe "base"
    chef.add_recipe "mysql56"
    chef.add_recipe "php55"

    chef.json = {
      httpd: {
        port: 80,
        docroot: "/vagrant/app/webroot"
      },
      php: {
        timezone: "Asia/Tokyo"
      },
      mysql: {
        password: ''
      },
    }
  end
end
