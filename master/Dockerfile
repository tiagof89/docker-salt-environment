FROM ubuntu:16.04

ENV SALT_VERSION=2016.3.1+ds-1

ADD start.sh /bin/start.sh

RUN apt-get update \
  && apt-get install -y vim-nox curl \
  && curl -L https://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest/SALTSTACK-GPG-KEY.pub | apt-key add - \
  && echo "deb http://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest xenial main" > /etc/apt/sources.list.d/saltstack.list \
  && apt-get update \
  && apt-get install -y salt-master=${SALT_VERSION}* salt-minion=${SALT_VERSION}* \
  && mkdir -p /etc/salt/minion.d \
  && echo "master: master" > /etc/salt/minion.d/masters.conf \
  && sed -i -e 's/#hash_type.*/hash_type: sha256/' /etc/salt/minion \
  && sed -i -e 's/#default_include.*/default_include: master.d\/\*.conf/' /etc/salt/master \
  && sed -i -e 's/#user.*/user: root/' /etc/salt/master \
  && sed -i -e 's/#hash_type.*/hash_type: sha256/' /etc/salt/master \
  && echo "auto_accept: True" > /etc/salt/master.d/auto_sign.conf \
  && echo "interface: 0.0.0.0\n\nfile_roots:\n  base:\n    - /srv/salt/state\n\npillar_roots:\n  base:\n    - /srv/salt/pillar\n" > /etc/salt/master.d/backends.conf \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

EXPOSE 4505 4506

ENTRYPOINT ["/bin/start.sh"]
