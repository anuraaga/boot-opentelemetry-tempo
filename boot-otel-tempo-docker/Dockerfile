FROM openjdk:8-jdk-alpine
#ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk

#ENV PATH $PATH:$JAVA_HOME/bin
#ENV JAVA_VERSION 8u212
#ENV JAVA_ALPINE_VERSION 8.212.04-r0

#RUN apk add --no-cache openjdk8="$JAVA_ALPINE_VERSION"

ENV OTEL_VERSION 0.15.0
ENV OTEL_JAR_FILE opentelemetry-javaagent-all.jar

ENV APP_HOME /app/bin

RUN mkdir -p ${APP_HOME}

COPY ./scripts/start-app.sh ${APP_HOME}/
COPY ./agent/${OTEL_JAR_FILE} ${APP_HOME}/

#USER root
#RUN chown -R 1001:1001 ${APP_HOME}
#RUN ["chmod", "+x", "/app/bin/start-app.sh"]

#USER 1001

ENV MIN_HEAP_SIZE="40M" MAX_HEAP_SIZE="512M" THREADSTACK_SIZE="228k" \
    JAVA_GC_ARGS="-XX:MinHeapFreeRatio=20 -XX:MaxHeapFreeRatio=40 -XX:+UseSerialGC -XX:GCTimeRatio=4 -XX:AdaptiveSizePolicyWeight=90" \
    JAVA_OPTS="-XX:MaxRAM=768m -server -Duser.timezone=America/Chicago -Djava.security.egd=file:/dev/./urandom -XX:CompressedClassSpaceSize=64m -XX:MaxMetaspaceSize=256m" \
    JAVA_DIAG_ARGS="" JAVA_OPTS_APPEND=""


#ENTRYPOINT [ "./start-app.sh" ]

CMD ["sh", "/app/bin/start-app.sh"]
