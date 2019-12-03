# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'json'

vconfig = JSON.parse(File.read(File.join(File.dirname(__FILE__), 'json/vconfig.json')))

Vagrant.configure("2") do |config|

  vconfig.each do |vcfg|
    config.vm.define vcfg['name'] do |vc|
      vc.vm.box = vcfg['box']
      vc.vm.hostname = vcfg['name']
      vc.vm.network "forwarded_port", guest: vcfg['guest_port'], host: vcfg['host_port']
      vc.vm.network "private_network", ip: vcfg['ip_addr']
      vc.vm.provider vcfg['vm'] do |vb|
        vb.memory = vcfg['memory']
        vb.cpus = vcfg['cpus']
      end

      config.vm.provision "shell", inline: "python --version || { apt-get update; apt-get install python -y;}"

      vc.vm.provision "ansible_local" do |ansible|
        ansible.limit = "all"
        ansible.playbook = vcfg['playbook']
        ansible.inventory_path = vcfg['hosts']
        ansible.install_mode = "pip"
        ansible.version = "2.5.5"

      end
    end
  end
end
