FROM debian:11

COPY sources.list /etc/apt/sources.list

# 定义默认 etcdctl api 版本
ENV ETCDCTL_API=3

RUN set -eux; \
        \
    apt-get update; \
        \
    apt-get -y install net-tools inetutils-ping procps curl; \
        \
    cd /tmp; \
    curl -sSL -o "etcd-v3.4.25-linux-amd64.tar.gz" "https://github.com/etcd-io/etcd/releases/download/v3.4.25/etcd-v3.4.25-linux-amd64.tar.gz"; \
    tar -xvf etcd*; \
    rm -rf *.gz; \
    cd etcd*; \
    cp -a ./etcd* /usr/local/bin/; \
    cd /tmp; \
    rm -rf *; \
    chmod +x /usr/local/bin/etcd*; \
        \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*;

ENTRYPOINT [ "etcd" ]

# CMD [ "--logger=zap" ]
