# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.define "foo", autostart: false do |foo|
    foo.vm.box = "ubuntu/trusty64"
    foo.vm.network "private_network", ip: "192.168.50.10"
    foo.vm.network :forwarded_port, guest: 22, host: 2200, auto_correct: false, id: "ssh"
  end
  # config.vm.define "bar", autostart:false do |bar|
  #   bar.vm.box = "ubuntu/trusty64"
  #   bar.vm.network "private_network", ip: "192.168.50.2"
  #   bar.vm.network :forwarded_port, guest: 22, host: 2201, auto_correct: false, id: "ssh"
  # end
  # config.vm.define "baz", autostart: false do |baz|
  #   baz.vm.box = "ubuntu/trusty64"
  #   baz.vm.network "private_network", ip: "192.168.50.3"
  #   baz.vm.network :forwarded_port, guest: 22, host: 2203, auto_correct: false, id: "ssh"
  # end
end
