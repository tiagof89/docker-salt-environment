FROM ubuntu:14.04.3

ENV SALT_VERSION=2015.8.3+ds-1

ADD start.sh /bin/start.sh

RUN apt-get update \
  && apt-get install -y vim-nox curl \
  && curl -L https://repo.saltstack.com/apt/ubuntu/ubuntu14/latest/SALTSTACK-GPG-KEY.pub | apt-key add - \
  && echo "deb http://repo.saltstack.com/apt/ubuntu/ubuntu14/latest trusty main" > /etc/apt/sources.list.d/saltstack.list \
  && apt-get update \
  && apt-get install -y salt-master=${SALT_VERSION}* salt-minion=${SALT_VERSION}* \
  && mkdir -p /etc/salt/minion.d \
  && echo "master: master\n" > /etc/salt/minion.d/masters.conf \
  && echo "auto_accept: True" > /etc/salt/master.d/auto_sign.conf \
  && echo "interface: 0.0.0.0\n\nfile_roots:\n  base:\n    - /srv/salt/state\n\npillar_roots:\n  base:\n    - /srv/salt/pillar\n" > /etc/salt/master.d/backends.conf \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

# stack is not yet released - but we need it
RUN cd /usr/lib/python2.7/dist-packages/salt/pillar/ \
  && curl -LO https://raw.githubusercontent.com/saltstack/salt/develop/salt/pillar/stack.py \
  && python -m py_compile stack.py

EXPOSE 4505 4506

ENTRYPOINT ["/bin/start.sh"]
