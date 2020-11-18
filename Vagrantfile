# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

# Check for missing plugins
  required_plugins = %w(vagrant-disksize vagrant-hostmanager vagrant-vbguest vagrant-clean)
  plugin_installed = false
  required_plugins.each do |plugin|
    unless Vagrant.has_plugin?(plugin)
      system "vagrant plugin install #{plugin}"
      plugin_installed = true
    end
  end
    # If new plugins installed, restart Vagrant process
  if plugin_installed === true
    exec "vagrant #{ARGV.join' '}"
  end
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.include_offline= true
  config.hostmanager.ignore_private_ip = false
  config.vm.box_check_update = false
  config.vbguest.auto_update = false
  config.vm.hostname = "archerysec.local"
  config.vm.network :private_network, ip: '192.168.20.2'
  config.disksize.size = '20GB'

  config.vm.provision "shell",privileged: true, inline: <<-SHELL
    sed -i s'/#prepend domain-name-servers 127.0.0.1/prepend domain-name-servers 8.8.8.8,8.8.4.4/' /etc/dhcp/dhclient.conf
    echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
    apt update
    apt install resolvconf -y
    systemctl start resolvconf.service
    systemctl enable resolvconf.service
    systemctl status resolvconf.service
    touch /etc/resolvconf/resolv.conf.d/head
    echo "nameserver 8.8.8.8" | sudo tee /etc/resolvconf/resolv.conf.d/head
    systemctl restart resolvconf.service
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.version = "2.9.15"
    ansible.playbook = "playbook.yml"
    ansible.verbose = true
  end
end
