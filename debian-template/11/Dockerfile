FROM docker.io/library/debian:11

# 中科大镜像源出问题时可以使用阿里云镜像源
COPY sources.list /etc/apt/sources.list

RUN set -eux; \
            \
        apt-get update; \
            \
        #......
            \
        # apt-get autoremove -y; \
        apt-get clean -y; \
        rm -rf /var/lib/apt/lists/*;
