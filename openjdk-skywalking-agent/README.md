## openjdk skywalking-agent
将skywalking-agent集成至openjdk镜像中。skywalk-agent相关的内容都存放与镜像中的路径：/sidecar/skywalking-agent  
因为skywalking-agent的配置文件高度封装系统环境变量，因此我们借助系统环境变量来完成对skywalking-agent的配置。

## Dockerfile变量声明
- SW_LOGGING_MAX_HISTORY_FILES="2"
  - 最大历史日志文件，如果日志文件超过此数量，最旧的文件将被删除；
- SW_LOGGING_DIR="/sidecar/skywalking-agent/logs"
  - skywalking-agent日志文件存储路径；
- SW_LOGGING_DIR="/sidecar/skywalking-agent/logs"
  - 是否开启收集SQL数据；
- AGENT_OPTS"
  - 需要配合K8s 编排文件使用。样例：-javaagent:/sidecar/skywalking-agent/skywalking-agent.jar;
- JAVA_OPTS"
  - 需要配合K8s 编排文件使用。样例：-jar /applications/spring-boot-helloworld.jar --server.port=80;

## 镜像构建
```
[root@k8s-master ~]# git clone https://github.com/shaxiaozz/Container-Image-Dockerfile.git
[root@k8s-master ~]# cd Container-Image-Dockerfile/openjdk-skywalking-agent
[root@k8s-master openjdk-skywalking-agent]# docker build . -t openjdk:11-jre-slim-buster-skywalking-agent-8.13.0
```

## K8s Deployment接入例子  
  - [ConfigMap资源](/k8s_example/configmap.yaml)
  - [Deployment资源](/k8s_example/deployment.yaml)

