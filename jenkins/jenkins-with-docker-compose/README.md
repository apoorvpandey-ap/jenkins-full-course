### Step-1 
### Step 1 : Version check
`docker --version `
`docker-compose --version`

### Step 2: Pull the jenkins image from the docker hub
docker pull jenkins/jenkins

### Step 3 : Write docker-compose.yml file 
```
docker-compose.yml 
version: '3'
services:
  jenkins:
    container_name: jenkins
    image: jenkins/jenkins
    ports:
      - "8080:8080"
    volumes:
      - "$PWD/Jenkns_home:/root/jenkins-data/jenkins_home"
    networks:
      - net
networks:
     net:
```

Step - 4 : UP compose file 
` docker-compose -f docker-compose.yml up -d`

Step -5 : docker logs
`docker logs <docker_id> `


Step - 6: check on the web
xx.xxx.xxx:8080




