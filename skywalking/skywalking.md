# Skywalking 服务链路追踪

---

## Skywalking 简介

> SkyWalking是一个开源的观测平台，用于从服务和云原生等基础设施中收集、分析、聚合以及可视化数据。SkyWalking 提供了一种简便的方式来清晰地观测分布式系统，甚至可以观测横跨不同云的系统。SkyWalking 更像是一种现代的应用程序性能监控（Application Performance Monitoring，即APM）工具，专为云原生，基于容器以及分布式系统而设计

项目地址： [Skywalking](https://github.com/apache/skywalking)  

SkyWalking是一个开源APM系统，包括对Cloud Native体系结构中的分布式系统的监视，跟踪，诊断功能。  

<p align="center">
<br><br>
<a target="_blank" rel="noopener noreferrer" href="https://camo.githubusercontent.com/72874858224f1be4f277d5e858c6cc63c785459927a4ab0c1dc63b7adeaea7b7/68747470733a2f2f6c616e6473636170652e636e63662e696f2f696d616765732f6c6566742d6c6f676f2e737667"><img src="https://camo.githubusercontent.com/72874858224f1be4f277d5e858c6cc63c785459927a4ab0c1dc63b7adeaea7b7/68747470733a2f2f6c616e6473636170652e636e63662e696f2f696d616765732f6c6566742d6c6f676f2e737667" width="150" data-canonical-src="https://landscape.cncf.io/images/left-logo.svg" style="max-width:100%;"></a>&nbsp;&nbsp;<a target="_blank" rel="noopener noreferrer" href="https://camo.githubusercontent.com/c5aee535d6f21df20c644791c2c999d670980166a9497e60b5bf2b496c902c6e/68747470733a2f2f6c616e6473636170652e636e63662e696f2f696d616765732f72696768742d6c6f676f2e737667"><img src="https://camo.githubusercontent.com/c5aee535d6f21df20c644791c2c999d670980166a9497e60b5bf2b496c902c6e/68747470733a2f2f6c616e6473636170652e636e63662e696f2f696d616765732f72696768742d6c6f676f2e737667" width="200" data-canonical-src="https://landscape.cncf.io/images/right-logo.svg" style="max-width:100%;"></a>
<br><br>
SkyWalking enriches the <a href="https://landscape.cncf.io/landscape=observability-and-analysis&amp;license=apache-license-2-0" rel="nofollow">CNCF CLOUD NATIVE Landscape.</a>
</p>
<p align="center">
<a href="https://openapm.io" rel="nofollow"><img src="https://camo.githubusercontent.com/02aa4229ce58d03b31aec4963deb4375962d08a2e002681da1c5594884454d38/68747470733a2f2f6f70656e61706d2e696f2f7374617469632f6d656469612f6f70656e61706d5f6c6f676f2e737667" width="100" data-canonical-src="https://openapm.io/static/media/openapm_logo.svg" style="max-width:100%;"></a>
  <br>Our project enriches the <a href="https://openapm.io" rel="nofollow">OpenAPM Landscape!</a>
</p>

核心功能如下:

* 服务，服务实例，端点指标分析
* 根本原因分析。在运行时分析代码
* 服务拓扑图分析
* 服务，服务实例和端点依赖关系分析
* 检测到慢速服务和端点
* 性能优化
* 分布式跟踪和上下文传播
* 数据库访问指标。检测慢速数据库访问语句（包括SQL语句）
* 警报
* 浏览器性能监控
* 基础架构（VM，网络，磁盘等）监控
* 跨指标，跟踪和日志的协作

SkyWalking 在逻辑上分为四部分：探针、平台后端、存储和用户界面。其架构图如下：

![skywalking架构](skywalking架构.png)

* 探针：基于不同的来源探针可能是不一样的，但作用都是收集数据，将数据格式化为 SkyWalking 适用的格式。例如在Java中则是做字节码植入，无侵入式的收集，并通过 HTTP 或者 gRPC 或者 消息 等方式发送数据到平台后端

* 平台后端：是一个支持集群模式运行的后台，用于数据聚合、数据分析以及驱动数据流从探针到用户界面的流程。平台后端还提供了各种可插拔的能力，如不同来源数据（如来自 Zipkin）格式化，不同存储系统以及集群管理。你甚至还可以使用观测分析语言来进行自定义聚合分析。

* 存储：是开放式的，可以选择一个既有的存储系统，如 ElasticSearch、H2 或 MySQL 集群（Sharding-Sphere 管理）等，也可以选择自己实现一个存储系统。

* 用户界面：也就是SkyWalking的可视化界面，UI非常炫酷且强大，同样它也是可定制以匹配你已存在的后端的

SkyWalking 为观察和监控分布式系统提供了许多不同场景下的解决方案。例如为Java、C#及Node.js提供语言自动探针，无侵入式的收集。同时也为一些编译型语言C++、GO等提供了手动打点 SDK。除此之外，还可以使用服务网格基础探针来收集数据，以帮助了解整个分布式系统。

* Java，.NET Core，NodeJS，PHP和Python 语言自动探针。
* Go和C ++ SDK。
* LUA代理，尤其适用于Nginx，OpenResty和Apache APISIX。
* 浏览器代理。
* 服务网格化观察、控制面板和数据面板。
* 度量系统接入，包括Prometheus，OpenTelemetry，Spring Sleuth（Micrometer），Zabbix。
* 日志。
* Zipkin v1 / v2跟踪。（无分析）

在SkyWalking中也存在服务、服务实例及端点概念，因为SkyWalking就是提供了这些概念的观测能力：

服务（Service）：表示对请求提供相同行为的一系列或一组工作负载。在使用打点代理或 SDK 的时候，你可以定义服务的名字。如果不定义的话，SkyWalking 将会使用你在平台上定义的名字，如 Istio。

服务实例（Service Instance）：上述的一组工作负载中的每一个工作负载称为一个实例。就像 Kubernetes 中的 pods 一样，服务实例未必就是操作系统上的一个进程。但当你在使用打点代理的时候， 一个服务实例实际就是操作系统上的一个真实进程。

端点（Endpoint）：对于特定服务所接收的请求路径，如 HTTP 的 URI 路径和 gRPC 服务的类名 + 方法签名

__Skywalking 主要优势__：

多种监控手段，语言探针和服务网格（Service Mesh）  
模块化，UI、存储、集群管理多种机制可选  
支持告警  
优秀的可视化方案  
社区活跃

## 搭建Skywalking 

### OAP & UI  

docker swarm 脚本如下：

``` yml

# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# source from https://github.com/apache/skywalking-docker/blob/master/8/8.5.0/compose-es7/docker-compose.yml
# by tecyang
# 2020-11-10

version: "3.4"
services:
  oap1:
    image: harbor.66123123.com/library/skywalking-oap-server:8.5.0-es7
    deploy:
      resources:
        limits:
          memory: 2g
      placement:
        constraints:
          - node.labels.role == web
      mode: replicated
      replicas: 1
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
    # healthcheck:
    #   test: ["CMD-SHELL", "/skywalking/bin/swctl ch"]
    #   interval: 30s
    #   timeout: 10s
    #   retries: 3
    #   start_period: 40s
    restart: always
    # ports:
    #   - 11800:11800
    #   - 12800:12800
    environment:
      SW_STORAGE: elasticsearch7
      SW_STORAGE_ES_CLUSTER_NODES: es01:9200,es02:9200,es03:9200
      SW_ES_USER: elastic
      SW_ES_PASSWORD: leading20200810
      SW_STORAGE_ES_INDEX_SHARDS_NUMBER: 2
      SW_STORAGE_ES_INDEX_REPLICAS_NUMBER: 0
      SW_CLUSTER: zookeeper
      SW_CLUSTER_ZK_HOST_PORT: zookeeper1:8010,zookeeper2:8010,zookeeper3:8010
      # 修改grpc 配置
      SW_CORE_GRPC_POOL_QUEUE_SIZE: 40000
      SW_CORE_GRPC_THREAD_POOL_SIZE: 64
      # 自监控
      SW_PROMETHEUS_FETCHER_ACTIVE: 'true'
      SW_TELEMETRY: prometheus
      # 每2000个请求执行一次批量
      SW_STORAGE_ES_BULK_ACTIONS: 4000
      # 每 20mb 刷新一次内存块
      SW_STORAGE_ES_BULK_SIZE: 40
      # 无论请求的数量如何，每10秒刷新一次堆
      SW_STORAGE_ES_FLUSH_INTERVAL: 30
      # 并发请求的数量
      SW_STORAGE_ES_CONCURRENT_REQUESTS: 4
      # elasticsearch 查询的最大数量
      SW_STORAGE_ES_QUERY_MAX_SIZE: 8000
      # elasticsearch 查询段最大数量
      # SW_STORAGE_ES_QUERY_SEGMENT_SIZE: 200
      # 采样率 50%
      SW_TRACE_SAMPLE_RATE: 5000
      JAVA_OPTS: " -Xmx1g -Xms1g "
    volumes:
      - /etc/localtime:/etc/localtime
      - /etc/timezone:/etc/timezone
      - ./config/alarm-settings.yml:/skywalking/config/alarm-settings.yml
    networks:
      swarm_net:
        aliases:
          - oap1
  oap2:
    image:  harbor.66123123.com/library/skywalking-oap-server:8.5.0-es7
    deploy:
      resources:
        limits:
          memory: 2g
      placement:
        constraints:
          - node.labels.role == web
      mode: replicated
      replicas: 1
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
    # healthcheck:
    #   test: ["CMD-SHELL", "/skywalking/bin/swctl ch"]
    #   interval: 30s
    #   timeout: 10s
    #   retries: 3
    #   start_period: 40s
    restart: always
    # ports:
    #   - 11800:11800
    #   - 12800:12800
    environment:
      SW_STORAGE: elasticsearch7
      SW_STORAGE_ES_CLUSTER_NODES: es01:9200,es02:9200,es03:9200
      SW_ES_USER: elastic
      SW_ES_PASSWORD: leading20200810
      SW_STORAGE_ES_INDEX_SHARDS_NUMBER: 2
      SW_STORAGE_ES_INDEX_REPLICAS_NUMBER: 0
      SW_CLUSTER: zookeeper
      SW_CLUSTER_ZK_HOST_PORT: zookeeper1:8010,zookeeper2:8010,zookeeper3:8010
      # 修改grpc 配置
      SW_CORE_GRPC_POOL_QUEUE_SIZE: 40000
      SW_CORE_GRPC_THREAD_POOL_SIZE: 64
      # 自监控
      SW_PROMETHEUS_FETCHER_ACTIVE: 'true'
      SW_TELEMETRY: prometheus
      # 每2000个请求执行一次批量
      SW_STORAGE_ES_BULK_ACTIONS: 4000
      # 每 20mb 刷新一次内存块
      SW_STORAGE_ES_BULK_SIZE: 40
      # 无论请求的数量如何，每10秒刷新一次堆
      SW_STORAGE_ES_FLUSH_INTERVAL: 30
      # 并发请求的数量
      SW_STORAGE_ES_CONCURRENT_REQUESTS: 4
      # elasticsearch 查询的最大数量
      SW_STORAGE_ES_QUERY_MAX_SIZE: 8000
      # elasticsearch 查询段最大数量
      # SW_STORAGE_ES_QUERY_SEGMENT_SIZE: 200
      # 采样率 50%
      SW_TRACE_SAMPLE_RATE: 5000
      JAVA_OPTS: " -Xmx1g -Xms1g "
    volumes:
      - /etc/localtime:/etc/localtime
      - /etc/timezone:/etc/timezone
      - ./config/alarm-settings.yml:/skywalking/config/alarm-settings.yml
    networks:
      swarm_net:
        aliases:
          - oap2
  oap3:
    image:  harbor.66123123.com/library/skywalking-oap-server:8.5.0-es7
    deploy:
      resources:
        limits:
          memory: 2g
      placement:
        constraints:
          - node.labels.role == web
      mode: replicated
      replicas: 1
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
    restart: always
    # healthcheck:
    #   test: ["CMD-SHELL", "/skywalking/bin/swctl ch"]
    #   interval: 30s
    #   timeout: 10s
    #   retries: 3
    #   start_period: 40s
    # ports:
    #   - 11800:11800
    #   - 12800:12800
    environment:
      SW_STORAGE: elasticsearch7
      SW_STORAGE_ES_CLUSTER_NODES: es01:9200,es02:9200,es03:9200
      SW_ES_USER: elastic
      SW_ES_PASSWORD: leading20200810
      SW_STORAGE_ES_INDEX_SHARDS_NUMBER: 2
      SW_STORAGE_ES_INDEX_REPLICAS_NUMBER: 0
      SW_CLUSTER: zookeeper
      SW_CLUSTER_ZK_HOST_PORT: zookeeper1:8010,zookeeper2:8010,zookeeper3:8010
      # 修改grpc 配置
      SW_CORE_GRPC_POOL_QUEUE_SIZE: 40000
      SW_CORE_GRPC_THREAD_POOL_SIZE: 64
      # 自监控
      SW_PROMETHEUS_FETCHER_ACTIVE: 'true'
      SW_TELEMETRY: prometheus
      # 每2000个请求执行一次批量
      SW_STORAGE_ES_BULK_ACTIONS: 4000
      # 每 20mb 刷新一次内存块
      SW_STORAGE_ES_BULK_SIZE: 40
      # 无论请求的数量如何，每10秒刷新一次堆
      SW_STORAGE_ES_FLUSH_INTERVAL: 30
      # 并发请求的数量
      SW_STORAGE_ES_CONCURRENT_REQUESTS: 4
      # elasticsearch 查询的最大数量
      SW_STORAGE_ES_QUERY_MAX_SIZE: 8000
      # elasticsearch 查询段最大数量
      # SW_STORAGE_ES_QUERY_SEGMENT_SIZE: 200
      # 采样率 50%
      SW_TRACE_SAMPLE_RATE: 5000
      JAVA_OPTS: " -Xmx1g -Xms1g "
    volumes:
      - /etc/localtime:/etc/localtime
      - /etc/timezone:/etc/timezone
      - ./config/alarm-settings.yml:/skywalking/config/alarm-settings.yml
    networks:
      swarm_net:
        aliases:
          - oap3
  ui:
    image:  harbor.66123123.com/library/skywalking-ui:8.5.0
    deploy:
      resources:
        limits:
          memory: 2g
      mode: replicated
      replicas: 1
      # placement:
      #   constraints:
      #     - node.hostname == pp1
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
    container_name: ui
    depends_on:
      - oap1
      - oap2
      - oap3
    links:
      - oap1
      - oap2
      - oap3
    restart: always
    ports:
      - 12345:8080
    environment:
      SW_OAP_ADDRESS: oap1:12800,oap2:12800,oap3:12800
    volumes:
      - /etc/localtime:/etc/localtime
      - /etc/timezone:/etc/timezone
    networks:
      swarm_net:
        aliases:
          - ui

networks:
  swarm_net:
    external:
      name: swarm_net

```

### java agent 

``` initSkywalking.sh

#!/bin/bash

wget -c https://mirrors.bfsu.edu.cn/apache/skywalking/8.5.0/apache-skywalking-apm-es7-8.5.0.tar.gz
mkdir apm-es7-8.5.0
tar -zxvf apache-skywalking-apm-es7-8.5.0.tar.gz -C ./apm-es7-8.5.0

cp -rf ./apm-es7-8.5.0/apache-skywalking-apm-bin-es7/* /home/produce/nas/skywalking/
# 对应服务启动配置agent挂载目录

```

### skywalking 报警模板

``` yml

# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Sample alarm rules.
rules:
  # Rule unique name, must be ended with `_rule`.
  service_resp_time_rule:
    metrics-name: service_resp_time
    op: ">"
    threshold: 2000
    period: 10
    count: 3
    silence-period: 5
    # message: Response time of service {name} is more than 2000ms in 3 minutes of last 10 minutes.
    message: 服务{name}的响应时间在最近10分钟的3分钟内超过2000毫秒。
  service_sla_rule:
    # Metrics value need to be long, double or int
    metrics-name: service_sla
    op: "<"
    threshold: 8000
    # The length of time to evaluate the metrics
    period: 10
    # How many times after the metrics match the condition, will trigger alarm
    count: 2
    # How many times of checks, the alarm keeps silence after alarm triggered, default as same as period.
    silence-period: 3
    # message: Successful rate of service {name} is lower than 80% in 2 minutes of last 10 minutes
    message: 最近10分钟的2分钟内，{name}服务的成功率低于80％
  service_resp_time_percentile_rule:
    # Metrics value need to be long, double or int
    metrics-name: service_percentile
    op: ">"
    threshold: 2000,2000,2000,2000,2000
    period: 10
    count: 3
    silence-period: 5
    # message: Percentile response time of service {name} alarm in 3 minutes of last 10 minutes, due to more than one condition of p50 > 2000, p75 > 000, p90 > 2000, p95 > 2000, p99 > 2000
    message: 由于 p50> 2000，p75> 2000，p90> 2000，p95> 2000，p99> 2000 以上的一种情况，服务{name}的百分比响应时间在最近10分钟的3分钟内发出警报
  service_instance_resp_time_rule:
    metrics-name: service_instance_resp_time
    op: ">"
    threshold: 2000
    period: 10
    count: 2
    silence-period: 5
    # message: Response time of service instance {name} is more than 2000ms in 2 minutes of last 10 minutes
    message: 最近10分钟的2分钟内，服务实例{name}的响应时间超过2000ms
  database_access_resp_time_rule:
    metrics-name: database_access_resp_time
    threshold: 2000
    op: ">"
    period: 10
    count: 2
    # message: Response time of database access {name} is more than 2000ms in 2 minutes of last 10 minutes
    message: 最近10分钟的2分钟内，数据库访问{name}的响应时间超过2000ms
  endpoint_relation_resp_time_rule:
    metrics-name: endpoint_relation_resp_time
    threshold: 2000
    op: ">"
    period: 10
    count: 2
    # message: Response time of endpoint relation {name} is more than 2000ms in 2 minutes of last 10 minutes
    message: 最近10分钟的2分钟内，端点关系{name}的响应时间超过2000ms
#  Active endpoint related metrics alarm will cost more memory than service and service instance metrics alarm.
#  Because the number of endpoint is much more than service and instance.
#
#  endpoint_avg_rule:
#    metrics-name: endpoint_avg
#    op: ">"
#    threshold: 1000
#    period: 10
#    count: 2
#    silence-period: 5
#    message: Response time of endpoint {name} is more than 1000ms in 2 minutes of last 10 minutes

dingtalkHooks:
  textTemplate: |-
    {
      "msgtype": "text",
      "text": {
        "content": "Apache SkyWalking Alarm: \n %s."
      }
    }
  webhooks:
    - url: https://oapi.dingtalk.com/robot/send?access_token=8c317491242ad398ca54e56e326b8da7ffc3568c59212b0a772007071d355b9d
      secret: SEC608717a644ceee5f3818ce64a3b4fe4098442a46999df560524e27cf07f30004
# webhooks:
#  - https://oapi.dingtalk.com/robot/send?access_token=8c317491242ad398ca54e56e326b8da7ffc3568c59212b0a772007071d355b9d
#  - http://127.0.0.1/notify/
#  - http://127.0.0.1/go-wechat/
```

## Skywalking 功能介绍

Skywalking 收集了大量信息，基于默认提供UI进行功能介绍，主要分为如下几部分：

* 仪表盘
* 拓扑图
* 服务链路追踪功能
* 性能剖析
* 日志
* 告警

### 仪表盘

![仪表盘](仪表盘.png)
<!-- ![仪表盘](01.png) -->
![service](02.png)
![instance](03.png)
![Endpoint](04.png)

### 拓扑图

![拓扑图](05.png)

### 服务链路追踪功能


### 性能剖析

### 日志

### 告警