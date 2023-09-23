FROM debian:12

COPY sources.list /etc/apt/sources.list

RUN set -eux; \
        \
    # 清除默认仓库源 \
    mv /etc/apt/sources.list.d/*.sources /tmp; \
    apt-get update; \
    apt-get -y install wget; \
        \
    wget https://github.com/oliver006/redis_exporter/releases/download/v1.53.0/redis_exporter-v1.53.0.linux-amd64.tar.gz; \
    tar -xvf redis_exporter*.tar.gz; \
    rm -rf *.tar.gz; \
        \
    cd redis_exporter*; \
    install -v -o root -g root -m 0755 redis_exporter /usr/local/bin/; \
        \
    cd /; \
    rm -rf redis_exporter*; \
    apt-get -y remove wget;\
    apt-get -y autoremove; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*;

ENTRYPOINT [ "redis_exporter" ]


###
# 构建命令
#   docker build --network=host -t ting24678/redis-exporter:1.53.0 ./
###
