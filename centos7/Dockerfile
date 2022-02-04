FROM centos:7

# Keepalived version
ARG KEEPALIVED_VERSION=2.2.7
WORKDIR /root
RUN yum install -y \
    autoconf \
    automake \
    file-devel \
    gcc \
    git \
    glib2-devel \
    json-c-devel \
    ipset-devel \
    iptables-devel \
    libmnl-devel \
    libnfnetlink-devel \
    libnftnl-devel \
    libnl3-devel \
    pcre2-devel \
    libsystemd-devel \
    make \
    net-snmp-devel \
    openssl-devel && yum clean all
RUN curl -o keepalived.tar.gz -SL http://keepalived.org/software/keepalived-${KEEPALIVED_VERSION}.tar.gz \
 && tar -xzf keepalived.tar.gz \
 && cd /root/keepalived-${KEEPALIVED_VERSION} \
 && ./configure --prefix=/opt/local \
 && make && make install \
 && rm -rf /root/keepalived.tar.gz /root/keepalived-${KEEPALIVED_VERSION}

RUN mkdir -p /etc/keepalived

VOLUME ["/etc/keepalived"]
CMD /bin/bash -c "/opt/local/sbin/keepalived --help && /opt/local/sbin/keepalived -f /etc/keepalived/keepalived.conf --dont-fork --log-console --log-detail --dump-conf"
