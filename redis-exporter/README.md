[TOC]

***

# \[ redis-exporter \] 

基于 [![](https://img.shields.io/badge/GitHub-oliver006/redis__exporter-green?logo=github)](https://github.com/oliver006/redis_exporter) 项目构建的 docker 镜像

该镜像的 github 地址 ( dockerfile 及构建脚本 ): https://github.com/ting24678/dockerfile/tree/main/redis-exporter

# 可选参数

|    环境变量    | 对应启动参数(CMD) |                             作用                             |
| :------------: | :---------------: | :----------------------------------------------------------: |
|   REDIS_ADDR   |   --redis.addr    | 指定要监控的 redis 地址，默认: 127.0.0.1:6379，redis://localhost:6379 |
|   REDIS_USER   |   --redis.user    |                指定 redis 用户，默认: default                |
| REDIS_PASSWORD | --redis.password  |                  指定 redis 密码，默认为空                   |

# Demo

## docker-cli 启动

```shell
docker run -d \
  --name=redis-exporter \
  --restart=always \
  --network=host \
  -e REDIS_ADDR="127.0.0.1:6379" \
  -e REDIS_USER="default" \
  -e REDIS_PASSWORD="redis.123" \
  -v /usr/share/zoneinfo/Asia/Shanghai:/etc/localtime \
  ting24678/redis-exporter:1.53.0
```

## docker-compose 启动

清单地址: https://github.com/ting24678/docker-compose/tree/main/redis-exporter 

```yaml
version: '3.8'
services:
  redis-exporter:
    image: ting24678/redis-exporter:1.53.0
    restart: always
    environment:
      REDIS_ADDR: 127.0.0.1:6379
      REDIS_USER: default
      REDIS_PASSWORD: redis.123
    network_mode: host
    # ports:
    # - 9121:9121
    volumes:
    - /usr/share/zoneinfo/Asia/Shanghai:/etc/localtime:ro
```

# Prometheus 发现配置

```yaml
# 监控单个 redis 实例 ( redis 信息在 redis-exporter 中配置, 也可以在此处配置 )
scrape_configs:
- job_name: "redis-01"
  static_configs:
  - targets:
    - 10.11.12.51:9121
  # file_sd_configs:
  # - files:
  #   - /etc/prometheus/file_sd/redis.yaml
  metric_relabel_configs:
  - source_labels:
    - __name__
    regex: "go_.*"
    action: drop

# 一个 redis-exporter 监控多个 redis 实例 ( 多个实例只能使用一个密码, 密码通过 redis-exporter 配置 )
scrape_configs:
- job_name: "redis-stack-cluster-1"
  metrics_path: /scrape
  static_configs:
  - targets:
    - 10.11.12.51:6379
    - 10.11.12.52:6379
    - 10.11.12.53:6379
  # file_sd_configs:
  # - files:
  #   - /etc/prometheus/file_sd/redis.yaml
  relabel_configs:
  - source_labels: [__address__]
    target_label: __param_target
  - source_labels: [__param_target]
    target_label: instance
  - target_label: __address__
    # redis-exporter 实例地址
    replacement: 10.11.12.51:9121
  metric_relabel_configs:
  - source_labels:
    - __name__
    regex: "go_.*"
    action: drop
```

# Grafana 面板推荐

- 763

