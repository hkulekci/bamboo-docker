FROM debian:latest

ENV BAMBOO_VERSION "5.15.4"

# Installing Java and Bamboo
RUN apt-get update && apt-get install wget software-properties-common -y
RUN add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main"
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get update && apt-get install oracle-java8-installer -y --allow-unauthenticated

RUN mkdir -p /opt/atlassian
WORKDIR /opt/atlassian
RUN wget https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-$BAMBOO_VERSION.tar.gz \
    && tar xzf atlassian-bamboo-$BAMBOO_VERSION.tar.gz

# Configure Bamboo
RUN mkdir /home/bamboo
RUN ln -s /opt/atlassian/atlassian-bamboo-$BAMBOO_VERSION /opt/atlassian/current
RUN echo "bamboo.home=/data/atlassian/application-data/bamboo" > current/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties
EXPOSE 8085:8085

WORKDIR /opt/atlassian/current
CMD bin/start-bamboo.sh -fg
