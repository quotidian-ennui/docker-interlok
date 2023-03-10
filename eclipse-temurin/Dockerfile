FROM eclipse-temurin:11-jdk

ARG java_tool_opts
ENV JAVA_TOOL_OPTIONS=$java_tool_opts


RUN \
    DEBIAN_FRONTEND=noninteractive apt-get -y -qq update && \
    DEBIAN_FRONTEND=noninteractive apt-get --no-install-recommends -y -qq install curl bash unzip ca-certificates gosu && \
    groupadd -r interlok && \
    useradd -r -g interlok interlok && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /opt/interlok/logs && \
    gosu nobody true

COPY scripts/gosu-docker-entrypoint.sh /docker-entrypoint.sh
WORKDIR /opt/interlok
COPY builder /root/builder

RUN  \
    chmod +x /docker-entrypoint.sh && \
    cd /root/builder && \
    chmod +x /root/builder/gradlew && \
    ./gradlew --no-watch-fs --no-daemon -PinterlokDistDirectory=/opt/interlok installDist && \
    rm -rf /root/.gradle && \
    rm -rf /root/builder

ENV JVM_ARGS=-Xmx1024m
ENV JAVA_OPTS=-Dsun.net.inetaddr.ttl=30
ENV INTERLOK_OPTS=bootstrap.properties
ENV INTERLOK_BASE=/opt/interlok
ENV JAVA_TOOL_OPTIONS=""

ENTRYPOINT ["/docker-entrypoint.sh"]
