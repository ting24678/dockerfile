FROM debian:11

ENV TINI_VERSION v0.19.0

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini

RUN set -eux; \
        \
    chmod +x /usr/bin/tini;

ENTRYPOINT [ "tini", "--" ]

# CMD [ "/bin/bash", "-c", "tail -f /dev/null" ]


###
# 构建命令:
#   docker build --network=host -t ting24678/tini:0.19.0-debian ./
###
