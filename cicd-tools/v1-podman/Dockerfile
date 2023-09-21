FROM debian:12

# 中科大镜像源出问题时可以使用阿里云镜像源
COPY sources.list /etc/apt/sources.list

RUN set -eux; \
        \
    > /etc/apt/sources.list.d/debian.sources; \
    apt-get update; \
    apt-get install -y curl git; \
        \
    curl -SL -o "podman-remote-static.tar.gz" "https://github.com/containers/podman/releases/download/v3.4.4/podman-remote-static.tar.gz"; \
    tar -xvf podman*; \
    rm -rf *.gz; \
    mv podman* /usr/bin/podman; \
    chmod +x /usr/bin/podman; \
        \
    curl -SL -o "/usr/bin/kubectl" "https://dl.k8s.io/release/v1.26.3/bin/linux/amd64/kubectl"; \
    chmod +x /usr/bin/kubectl; \
        \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*;

###
# 构建命令
#   podman build --network=host -t ting24678/cicd-tools:v1-podman ./
###
