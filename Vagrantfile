# -*- mode: ruby -*-
# vi: set ft=ruby :

WORKER_IP = "192.168.151.120"

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false

   if Vagrant.has_plugin?('landrush')
     config.landrush.enabled = true
     config.landrush.tld = 'worker.com'
     config.landrush.guest_redirect_dns = false
   end


  config.vm.provision "shell", inline: <<-SHELL
    chmod +x /vagrant/*.sh
    /vagrant/worker.sh
  SHELL

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus   = "1"
  end

  config.vm.define "worker" do |node|
    node.vm.network "private_network", ip: "#{WORKER_IP}"
    node.vm.hostname = "vm.worker.com"
  end
end
