Docker templates
=================

Running docker containers in virtualbox which is maintained by Vagrant.

1. Hello world
2. Zookeeper
3. Kafka with zookeeper
4. Java application template
5. Spark standalone for development, the UI will be available at 8081 at your machine

Start Vagrant, rebuild Vagrant (at the current git repo dir, it will be mounted to /vagrant dir in guest machine)
---------------

	vagrant init precise64 http://files.vagrantup.com/precise64.box
	vagrant up
	vagrant reload
	vagrant plugin install vagrant-vbguest

Install Docker at guest machine
----------------

	vagrant ssh
	sudo apt-get update
	sudo apt-get install linux-image-generic-lts-raring linux-headers-generic-lts-raring curl
	sudo reboot
	sudo sh -c "curl https://get.docker.io/gpg | apt-key add -"
	sudo sh -c "echo deb http://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
	sudo apt-get update
	sudo apt-get install lxc-docker

Start Kafka
----------------

	vagrant ssh
	cd /vagrant/kafka
	sudo docker build -t bruce/kafka .
	./start.sh

Useful Docker commands
----------------

	sudo docker ps
	sudo docker images
	sudo docker tag xxxxxxxx bruce/kafka
	sudo docker run -t -i xxxxxxxx bash
	sudo docker build -t bruce/hello .
	sudo docker stop xxxxxxxx
