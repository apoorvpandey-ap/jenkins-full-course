### Step -1 Create Dockerfile
```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:mypassword' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
```
### Step -2  docker build
`docker build -t sshd_tagged_image .`

### Step -3 Run image 

`docker run -d -P --name test_sshd_container sshd_tagged_image`

### Step -4 Put the port out from the container
` docker port test_sshd_container`
`docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' test_sshd_container
`
### Step -5 Finally, now that you have the IP address to SSH to, try to SSH to the container, and it should work!

ssh root@Ip-Address-of-the-container 

