VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end
  
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :forwarded_port, host: 8888, guest: 8888
  config.vm.network :forwarded_port, host: 2181, guest: 2181
  config.vm.network :forwarded_port, host: 9092, guest: 9092

  config.vm.network :forwarded_port, host: 9999, guest: 8080
  config.vm.network :forwarded_port, host: 7077, guest: 7077
  config.vm.network :forwarded_port, host: 6066, guest: 6066
  config.vm.network :forwarded_port, host: 8081, guest: 8081
  config.vm.network :forwarded_port, host: 4040, guest: 4040


end