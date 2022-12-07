FROM openjdk:11-jre-slim-buster
ADD apache-skywalking-java-agent-8.13.0.tgz /sidecar
RUN cp -a /sidecar/skywalking-agent/optional-plugins/apm-trace-ignore-plugin-8.13.0.jar /sidecar/skywalking-agent/plugins/ && \
    echo 'trace.ignore_path=${TRACE_IGNORE_PATH:/metrics/**,GET:/metrics/**,GET:/actuator/prometheus,/actuator/prometheus,GET:/actuator/health,/actuator/health,/services/healthCheck,Zookeeper/WatchedEvent/**,/eureka/**}' >> /sidecar/skywalking-agent/config/apm-trace-ignore-plugin.config && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    sed -i -e "s/security.debian.org/mirrors.ustc.edu.cn/" -e "s/deb.debian.org/mirrors.ustc.edu.cn/" /etc/apt/sources.list && \
    apt-get update  && \
    apt-get install --no-install-recommends -y iputils-ping iproute2 dnsutils net-tools vim telnet netcat procps lsof tcpdump cron jq && \
    apt-get autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "Asia/Shanghai" > /etc/timezone
ENV SW_LOGGING_MAX_HISTORY_FILES="2" \
    SW_LOGGING_DIR="/sidecar/skywalking-agent/logs" \
    SW_JDBC_TRACE_SQL_PARAMETERS=true
CMD ["bash","-c","java -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap ${AGENT_OPTS} ${JAVA_OPTS}"]