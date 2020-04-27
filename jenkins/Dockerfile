FROM jenkins/jenkins:lts
USER root


RUN apt-get update && apt-get -y install rsync

#This download the docker client so we can connect 
#to the socket of docker from then container.

RUN mkdir -p /tmp/download && \
 curl -L https://download.docker.com/linux/static/stable/x86_64/docker-18.03.1-ce.tgz | tar -xz -C /tmp/download && \
 rm -rf /tmp/download/docker/dockerd && \
 mv /tmp/download/docker/docker* /usr/local/bin/ && \
 rm -rf /tmp/download && \
 groupadd -g 999 docker && \


 #Adding user jenkins to group docker and staff.
 # This way, user jenkins inside the container
 # will be able to execute docker.sock, because
 #this belogns to docker group too in the host.

 usermod -aG staff,docker jenkins

USER jenkins