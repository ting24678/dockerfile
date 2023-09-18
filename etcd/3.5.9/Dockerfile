FROM debian:12

# 配置国内镜像源
COPY sources.list /etc/apt/sources.list

# 定义默认 etcdctl api 版本
ENV ETCDCTL_API=3

RUN set -eux; \
        \
    # 清除默认仓库源
    > /etc/apt/sources.list.d/debian.sources; \
    apt-get update; \
        \
    apt-get -y install net-tools inetutils-ping procps curl; \
        \
    cd /tmp; \
    curl -sSL -o "etcd-v3.5.9-linux-amd64.tar.gz" "https://github.com/etcd-io/etcd/releases/download/v3.5.9/etcd-v3.5.9-linux-amd64.tar.gz"; \
    tar -xvf etcd*; \
    rm -rf *.gz; \
    cd etcd*; \
    cp -a ./etcd* /usr/local/bin/; \
    cd /tmp; \
    rm -rf *; \
    chmod +x /usr/local/bin/etcd*; \
        \
    apt-get autoremove -y; \
    apt-get clean -y; \
    rm -rf /var/lib/apt/lists/*;

ENTRYPOINT [ "etcd" ]

# CMD [ "--logger=zap" ]

###
# 构建命令
#   docker build --network=host -t fufeng24678/etcd:3.5.9 .
###
