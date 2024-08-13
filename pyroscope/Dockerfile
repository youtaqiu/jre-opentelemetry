ARG JRE_VERSION=21
FROM debian:stable-slim AS base

RUN apt-get update && apt-get install -y curl grep

FROM base AS downloader

RUN LATEST_VERSION=$(curl -s https://api.github.com/repos/grafana/pyroscope-java/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")') \
    && curl -L -o /tmp/pyroscope.jar https://github.com/grafana/pyroscope-java/releases/download/$LATEST_VERSION/pyroscope.jar

FROM youtaqiu/jre:${JRE_VERSION}

RUN mkdir -p /app/lib
COPY --from=downloader /tmp/pyroscope.jar /app/lib/pyroscope.jar
