FROM jenkins/jenkins:lts
USER root
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update -qq \
    && apt-get -y install docker-ce
RUN curl -SL https://github.com/docker/compose/releases/download/v2.20.3/docker-compose-linux-x86_64 -o /usr/bin/docker-compose
RUN chmod +x /usr/bin/docker-compose \
    && usermod -aG docker jenkins \
    && chgrp docker /usr/local/bin/docker-compose \
    && chmod 750 /usr/local/bin/docker-compose