FROM ubuntu:16.04
MAINTAINER <emolwy@gmail.com>

SHELL ["/bin/sh", "-c"],

# Default to supporting utf-8
ENV LANG=C.UTF-8

# 使用阿里云软件包源
# Install required packages
RUN cp /etc/apt/sources.list /etc/apt/sources.list_backup \
    && echo 'deb-src http://archive.ubuntu.com/ubuntu xenial main restricted #Added by software-properties' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted' >> /etc/apt/sources.list \
    && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe #Added by software-properties' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted' >> /etc/apt/sources.list \
    && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe #Added by software-properties' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial universe' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse' >> /etc/apt/sources.list \
    && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse #Added by software-properties' >> /etc/apt/sources.list \
    && echo 'deb http://archive.canonical.com/ubuntu xenial partner' >> /etc/apt/sources.list \
    && echo 'deb-src http://archive.canonical.com/ubuntu xenial partner' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted' >> /etc/apt/sources.list \
    && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe #Added by software-properties' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse' >> /etc/apt/sources.list \
    && apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
      gcc \
      make \
      libc6-dev \
      perl \
      wget \
      apt-transport-https \
      vim \
      tzdata \
      nano \
      less \
    && rm -rf /var/lib/apt/lists/* 

# Remove MOTD
RUN rm -rf /etc/update-motd.d /etc/motd /etc/motd.dynamic
RUN ln -fs /dev/null /run/motd.dynamic

# Copy assets
COPY RELEASE /
COPY assets/ /assets/
RUN /assets/setup

# Allow to access embedded tools
ENV PATH /opt/gitlab/embedded/bin:/opt/gitlab/bin:/assets:$PATH

# Resolve error: TERM environment variable not set.
ENV TERM xterm

# Expose web & ssh
EXPOSE 443 80 22

# Define data volumes
VOLUME ["/etc/gitlab", "/var/opt/gitlab", "/var/log/gitlab"]

# Wrapper to handle signal, trigger runit and reconfigure GitLab
CMD ["/assets/wrapper"]

HEALTHCHECK --interval=60s --timeout=30s --retries=5 \
CMD /opt/gitlab/bin/gitlab-healthcheck --fail --max-time 10
