ARG JRE_VERSION=21
FROM debian:stable-slim AS base

RUN apt-get update && apt-get install -y curl grep

FROM base AS downloader

RUN LATEST_VERSION=$(curl -s https://api.github.com/repos/open-telemetry/opentelemetry-java-instrumentation/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")') \
    && curl -L -o /tmp/opentelemetry.jar https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/$LATEST_VERSION/opentelemetry-javaagent.jar

FROM youtaqiu/jre:${JRE_VERSION}

RUN mkdir -p /app/lib
COPY --from=downloader /tmp/opentelemetry.jar /app/lib/opentelemetry.jar
