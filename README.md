# kafka-manager-docker

How to use this image
Using docker
docker run -d \
     -p 9000:9000  \
     -e ZK_HOSTS="localhost:2181" \
     blueapple/kafka-manager-docker:latest \
     -Dpidfile.path=/dev/null


Using docker-compose


version: '3'

services:

  kafka_manager:
  
    image: blueapple/kafka-manager-docker:latest
    
    ports:
    
      - "9000:9000"
      
    environment:
    
      ZK_HOSTS: "zoo:2181"
      
      APPLICATION_SECRET: "random-secret"
      
    command: -Dpidfile.path=/dev/null
