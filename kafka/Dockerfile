FROM ubuntu

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y -q software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update -y
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install oracle-java7-installer -y
RUN apt-get -y -q install wget
RUN wget -q -O - http://mirror.vorboss.net/apache/kafka/0.8.1.1/kafka_2.8.0-0.8.1.1.tgz \
  | tar -C /opt -xz

RUN echo "deb http://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-get update
RUN apt-get -y install sbt git

RUN git clone https://github.com/yahoo/kafka-manager /opt/kafka-manager

WORKDIR /opt/kafka-manager

RUN sbt clean dist

WORKDIR /opt/kafka_2.8.0-0.8.1.1

RUN apt-get -y -q install supervisor

ADD zk.sh /opt/kafka_2.8.0-0.8.1.1/zk.sh
RUN chmod 755 /opt/kafka_2.8.0-0.8.1.1/zk.sh

ADD kafka.sh /opt/kafka_2.8.0-0.8.1.1/kafka.sh
RUN chmod 755 /opt/kafka_2.8.0-0.8.1.1/kafka.sh

ADD supervisor-zk.conf /etc/supervisor/conf.d/supervisor-zk.conf
ADD supervisor-kafka.conf /etc/supervisor/conf.d/supervisor-kafka.conf

EXPOSE 2181 9092

CMD ["supervisord", "-n"]
