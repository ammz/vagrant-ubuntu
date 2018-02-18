# -*- mode: ruby -*-

require_relative './vagrant/key_authorization'

Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/xenial64'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'
  {
    # 'db1'    => '192.168.33.10',
    'siaxe'  => '192.168.33.11',
    # 'redis1' => '192.168.33.12',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}.binfante.es"
    end
  end

  config.vm.synced_folder "~/proyectos", "/home/ubuntu/proyectos", owner: "ubuntu", group: "ubuntu"
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
    vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
    vb.customize ["modifyvm", :id, "--audio", "none"]
    vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
    vb.customize ["modifyvm", :id, "--nictype2", "virtio"]
  end
end
