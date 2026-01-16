FROM eclipse-temurin:25-jdk

ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

WORKDIR /opt/hytale
COPY Server/ /opt/hytale/

RUN mkdir -p /hytale

EXPOSE 5520/udp

ENV JAVA_OPTS="-Xms2G -Xmx4G"
ENV AOT_OPTS="-XX:AOTCache=/opt/hytale/HytaleServer.aot"

CMD java $JAVA_OPTS $AOT_OPTS -jar /opt/hytale/HytaleServer.jar --assets /opt/hytale/Assets.zip
