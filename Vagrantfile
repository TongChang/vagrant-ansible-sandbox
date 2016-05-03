# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty32"

  config.vm.define :manager do |node|
#    node.vm.box = "ubuntu/trusty32"
    node.vm.network :forwarded_port, guest: 22, host: 2001, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.11"
  end

  config.vm.define :rpi_1 do |node|
#    node.vm.box = "ubuntu/trusty32"
    node.vm.network :forwarded_port, guest: 22, host: 2011, id: "ssh"
    node.vm.network :forwarded_port, guest: 80, host: 8000, id: "http"
    node.vm.network :private_network, ip: "192.168.33.12"
  end

end
