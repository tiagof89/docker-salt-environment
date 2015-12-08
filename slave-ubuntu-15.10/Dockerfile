FROM ubuntu:15.10

ENV SALT_VERSION=2015.5.3+ds-1

ADD start.sh /bin/start.sh

RUN apt-get update \
  && apt-get install -y vim-nox curl software-properties-common \
  && add-apt-repository ppa:saltstack/salt \
  && apt-get install -y salt-minion=${SALT_VERSION}* \
  && mkdir -p /etc/salt/minion.d \
  && echo "master: master" > /etc/salt/minion.d/masters.conf \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

ENTRYPOINT ["/bin/start.sh"]
