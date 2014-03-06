Vagrant.configure("2") do |config|
  config.vm.box     = "coreos"
  config.vm.box_url = "http://storage.core-os.net/coreos/amd64-generic/dev-channel/coreos_production_vagrant.box"

  config.vm.network "private_network", ip: "172.12.8.150"

  config.vm.synced_folder ".", "/home/core/share",
                          id: "core",
                          nfs: true,
                          mount_options: ['nolock,vers=3,udp']

  config.vm.synced_folder "../volumes", "/home/core/volumes",
                          id: "volumes",
                          nfs: true,
                          mount_options: ['nolock,vers=3,udp']

  config.vm.provider :virtualbox do |vb, override|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.network :forwarded_port, guest: 4243, host: 4243

  (49000..49900).each do |port|
    config.vm.network :forwarded_port, host: port, guest: port
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end
end