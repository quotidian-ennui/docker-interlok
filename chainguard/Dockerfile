FROM bellsoft/liberica-openjdk-alpine:11 as build

COPY builder /root/builder

RUN  \
    cd /root/builder && \
    chmod +x /root/builder/gradlew && \
    ./gradlew --no-watch-fs --no-daemon -PinterlokDistDirectory=/opt/interlok installDist && \
    rm -rf /root/.gradle && \
    rm -rf /root/builder

FROM cgr.dev/chainguard/jdk:openjdk-jre-11

COPY --from=build /opt/interlok /app/

ENV JAVA_TOOL_OPTIONS="-Xmx1024m -Dsun.net.inetaddr.ttl=30"

CMD ["-jar", "lib/interlok-boot.jar" , "bootstrap.properties"]