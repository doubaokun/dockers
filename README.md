Docker templates
=================

Running docker containers in virtualbox which is maintained by Vagrant.

1. Hello world
2. Zookeeper
3. Kafka with zookeeper
4. Java application template

Start Vagrant, rebuild Vagrant
---------------

	vagrant init precise64 http://files.vagrantup.com/precise64.box
	vagrant up
	vagrant reload

Start Kafka
----------------

	vagrant ssh
	cd /vagrant
	./start.sh

Useful Docker commands
----------------

	sudo docker ps
	sudo docker images
	sudo docker tag xxxxxxxx bruce/kafka
	sudo docker run -t -i xxxxxxxx bash
	sudo docker build -t bruce/hello .
	sudo docker stop xxxxxxxx
