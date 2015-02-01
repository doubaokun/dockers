ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.provider "docker" do |d|
    d.build_dir = "."
    d.has_ssh    = true
    d.ports = ['8888:8888', '2181:2181']
  end

  config.vm.network :forwarded_port, host: 8888, guest: 8888
  config.vm.network :forwarded_port, host: 2181, guest: 2181

end