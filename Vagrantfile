# -*- mode: ruby -*-
# vi: set ft=ruby :
GLOBAL_BOX = "xanagi/centos-6.5-chef"
GLOBAL_CONFIG = {
  "mysql" => {
    "server_debian_password" => "123456",
    "server_root_password" => "123456",
    "server_repl_password" => "123456",
  },
    'pulse' => {
      'db_host' => '192.168.33.112'
    }
  }
Vagrant.configure(2) do |config|
  config.vm.define 'db' do |db|
    db.vm.box = GLOBAL_BOX
    db.vm.network "private_network", ip: "192.168.33.112"
     db.vm.provider "virtualbox" do |vb|
       vb.memory = "512"
     end
    db.berkshelf.enabled = true
    db.vm.provision "chef_solo" do |chef|

      chef.add_recipe "pulse::db-server"
      chef.json = GLOBAL_CONFIG
    end
  end
end

Vagrant.configure(2) do |config|
  config.vm.define 'app' do |app|
    app.vm.box = GLOBAL_BOX
    app.vm.network "private_network", ip: "192.168.33.111"
     app.vm.provider "virtualbox" do |vb|
       vb.memory = "1024"
     end
    app.berkshelf.enabled = true
    app.vm.provision "chef_solo" do |chef|

      chef.add_recipe "pulse::app-server"
      chef.json = GLOBAL_CONFIG
    end
  end
end

Vagrant.configure(2) do |config|
  config.vm.define 'web' do |web|
    web.vm.box = GLOBAL_BOX
    web.vm.network "private_network", ip: "192.168.33.113"
     web.vm.provider "virtualbox" do |vb|
       vb.memory = "256"
     end
    web.berkshelf.enabled = true
    web.vm.provision "chef_solo" do |chef|

      chef.add_recipe "pulse::web-server"
      chef.json = GLOBAL_CONFIG
    end
  end
end
