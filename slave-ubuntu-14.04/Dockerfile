FROM ubuntu:14.04.5

ENV SALT_VERSION=2016.3.1

ADD start.sh /bin/start.sh

RUN apt-get update \
  && apt-get install -y vim-nox curl \
  && curl -L https://repo.saltstack.com/apt/ubuntu/14.04/amd64/archive/${SALT_VERSION}/SALTSTACK-GPG-KEY.pub | apt-key add - \
  && echo "deb http://repo.saltstack.com/apt/ubuntu/14.04/amd64/archive/${SALT_VERSION} trusty main" > /etc/apt/sources.list.d/saltstack.list \
  && apt-get update \
  && apt-get install -y salt-minion=${SALT_VERSION}* \
  && mkdir -p /etc/salt/minion.d \
  && echo "master: master" > /etc/salt/minion.d/masters.conf \
  && sed -i -e 's/#hash_type.*/hash_type: sha256/' /etc/salt/minion \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean \
  && echo "testmode: true\n" > /etc/salt/grains

ENTRYPOINT ["/bin/start.sh"]
