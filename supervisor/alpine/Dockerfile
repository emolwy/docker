FROM alpine:latest
LABEL maintainer="emolwy <emolwy@gmail.com>"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk update && \
    apk add --no-cache supervisor ca-certificates && \
    mkdir /etc/supervisor.d/

COPY ./supervisord.conf /etc/supervisord.conf
COPY ./supervisor.d/ /etc/supervisor.d/

ENTRYPOINT ["/usr/bin/supervisord"]
