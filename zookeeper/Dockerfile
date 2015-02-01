FROM ubuntu
EXPOSE 2181

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y -q software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update -y
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install oracle-java7-installer -y
RUN apt-get -y -q install wget
RUN wget -q -O - http://mirrors.sonic.net/apache/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz \
  | tar -C /opt -xz

WORKDIR /opt/zookeeper-3.4.6/
ADD zoo.cfg /opt/zookeeper-3.4.6/conf/zoo.cfg
ENTRYPOINT ["./bin/zkServer.sh", "start-foreground"]