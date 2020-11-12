# -*- mode: ruby -*-
# vi: set ft=ruby :
$hostsfile_update = <<-'SCRIPT'
echo -e '192.168.56.110 control.example.com control\n192.168.56.111 node1.example.com node1\n192.168.56.112 node2.example.com node2' >> /etc/hosts
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config && systemctl restart sshd
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.define "control", primary: true do |control|
    control.vm.box = "centos/7"
    control.vm.hostname = "control.example.com"
    control.vm.network "forwarded_port", guest: 80, host: 8080
    control.vm.network "private_network", ip: "192.168.56.110"
    control.vm.provision "shell", inline: $hostsfile_update
    control.vm.provider "virtualbox" do |v|
 	v.memory = 4096
	v.cpus = 2
    end
  end
end
