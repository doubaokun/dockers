Docker templates
=================

Running docker containers in virtualbox which is maintained by Vagrant.

These docker templates is the quick way to setup your development environments including: Zookeeper, Kafka, Spark, or your custom application.

1. Hello world
2. Zookeeper
3. Kafka with zookeeper
4. Java application template
5. Spark standalone for development

Start Vagrant, rebuild Vagrant 
---------------

Run commands at the current git repo dir, it will be mounted to /vagrant dir in guest machine

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

Start zookeeper
----------------

	vagrant ssh
	cd /vagrant/zookeeper
	sudo docker build -t bruce/zookeeper .
	./start.sh OR
	sudo docker run -d -p 2181:2181 bruce/zookeeper

Start Kafka
----------------

	vagrant ssh
	cd /vagrant/kafka
	sudo docker build -t bruce/kafka .
	./start.sh OR
	sudo docker run -d -p 2181:2181 -p 9092:9092 bruce/kafka

Start Spark
----------------

The spark UI will be available at 8081 at your machine.

	vagrant ssh
	cd /vagrant/spark
	sudo docker build -t bruce/spark .
	./start.sh OR
	sudo docker run -d -p 6066:6066 -p 7077:7077 -p 8080:8080 -p 8081:8081 -p 4040:4040 -v /vagrant/data:/vagrant/data bruce/spark

Submit application to spark cluster

	./bin/spark-submit \
	--class org.apache.spark.examples.SparkPi \
	--master spark://127.0.0.1:6066 \
	--deploy-mode cluster \
	--driver-memory 128m  \
	--executor-memory 128m   \
	--executor-cores 1 \
	/vagrant/data/spark-examples_2.10-1.3.0-SNAPSHOT.jar \
	10

Run spark application

	./bin/spark-submit \
	--class org.apache.spark.examples.SparkPi \
	--master local\[2\] \
	/vagrant/data/spark-examples_2.10-1.3.0-SNAPSHOT.jar \
	10

Useful Docker commands
----------------

	sudo docker ps
	sudo docker images
	sudo docker tag xxxxxxxx bruce/kafka
	sudo docker run -t -i xxxxxxxx bash
	sudo docker build -t bruce/hello .
	sudo docker stop xxxxxxxx
