# Kafka Manager Dockerfile
[Kafka Manager](https://github.com/yahoo/kafka-manager) is a tool for managing [Apache Kafka](http://kafka.apache.org) developed by [Yahoo Inc](https://www.yahoo.com).

## Description
The latest version of the docker image is based on:  

* docker image - [oraclelinux:6.8](https://hub.docker.com/_/oraclelinux/)  
* java - [JDK 1.8.0_131](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  
* kafka manager - [1.3.3.18](https://github.com/yahoo/kafka-manager/releases/tag/1.3.3.18)

The following actions will be performed during building a docker image:  

* install the additional packages (git, wget, tar, vim, mc, unzip, lsof)  
* kafka-manager home set to /opt/kafka-manager  
* delete all unused files (README.md bin/*.bat share/)  
* change debug level from INFO/WARN to ERROR into logback.xml and logger.xml files  
* set kafka-manager client port to 9000  
* define application.home -Dapplication.home=./  
* define ZK\_HOST=localhost:2181  
* export JAVA\_HOME  
* set TERM=xterm  

## How to use this image
Using docker
docker run -d \
     -p 9000:9000  \
     -e ZK_HOSTS="localhost:2181" \
     hlebalbau/kafka-manager:latest \
     -Dpidfile.path=/dev/null

Using docker-compose
version: '3.6'
services:
  kafka_manager:
    image: hlebalbau/kafka-manager:latest
    ports:
      - "9000:9000"
    environment:
      ZK_HOSTS: "zoo:2181"
      APPLICATION_SECRET: "random-secret"
      command: -Dpidfile.path=/dev/null
