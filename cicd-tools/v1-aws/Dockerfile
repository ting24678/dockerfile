FROM ting24678/cicd-tools:v1

RUN set -eux; \
        \
    apt-get update; \
    apt-get install -y curl git zip less; \
        \
    curl -SL -o "awscliv2.zip" "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip"; \
    unzip awscliv2.zip; \
    ./aws/install; \
    rm -rf aws*; \
        \
    apt-get remove -y zip; \
    apt-get autoremove -y; \
    apt-get clean -y; \
    rm -rf /var/lib/apt/lists/*;

###
# 构建命令
#   docker build --network=host -t ting24678/cicd-tools:v1-aws ./
###
