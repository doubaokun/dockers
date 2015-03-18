FROM ubuntu

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y -q software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update -y
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install oracle-java7-installer -y
RUN apt-get -y -q install wget
RUN apt-get -y -q install git
RUN apt-get -y -q install scala
RUN wget -q -O - http://www.us.apache.org/dist/spark/spark-1.3.0/spark-1.3.0-bin-cdh4.tgz \
  | tar -C /opt -xzv

WORKDIR /opt/spark-1.3.0-bin-cdh4/

ADD spark-worker.sh /opt/spark-worker.sh
RUN chmod 755 /opt/spark-worker.sh

EXPOSE 8080 7077 6066

CMD /opt/spark-1.3.0-bin-cdh4/sbin/start-master.sh && /opt/spark-worker.sh