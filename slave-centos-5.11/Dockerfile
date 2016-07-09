FROM centos:centos5.11

ENV SALT_VERSION=2016.3.1-1.el5

ADD start.sh /bin/start.sh

RUN echo -e '[saltstack-repo]\nname=SaltStack repo for RHEL/CentOS$releasever\nbaseurl=https://repo.saltstack.com/yum/redhat/$releasever/$basearch/latest\nenabled=1\ngpgcheck=0\n' > /etc/yum.repos.d/saltstack.repo \
  && yum install -y salt-minion-${SALT_VERSION} epel-release \
  && mkdir -p /etc/salt/minion.d \
  && echo -e "master: master" > /etc/salt/minion.d/masters.conf \
  && rm -rf /var/lib/yum/* \
  && yum clean all \
  && echo -e "testmode: true\n" > /etc/salt/grains

ENTRYPOINT ["/bin/start.sh"]
