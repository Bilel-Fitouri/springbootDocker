FROM ubuntu:latest

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    apt-get clean

ADD springbootDocker-0.0.1-SNAPSHOT.jar /springbootDocker-0.0.1-SNAPSHOT.jar

EXPOSE 8080

CMD java -jar /springbootDocker-0.0.1-SNAPSHOT.jar
