FROM ubuntu

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y -q software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update -y
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install oracle-java7-installer -y

ADD app.jar /opt/app.jar

EXPOSE 8888

ENTRYPOINT ["java", "-jar", "/opt/app.jar"]