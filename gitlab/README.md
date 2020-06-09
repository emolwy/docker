The latest docker guide can be found here: [GitLab Docker images](/doc/docker/README.md).

#### 1、编辑RELEASE文件，指定软件版本 
````bash
ZLIB_VERSION=1.2.11
OPENSSL_VERSION=1.1.1g
OPENSSH_VERSION=8.3p1
RELEASE_PACKAGE=gitlab-ce
RELEASE_VERSION=13.0.1-ce.0
````
#### 2、编译镜像 
````bash
docker build -t ubuntu/gitlab-ce:13.0.1-ce.0 ./ >build.log 2>&1
# 编译时如发现下载软件包过慢，可编辑assets/setup文件，替换下载链接地址。
# wget --no-check-certificate --tries=5 https://www.zlib.net/zlib-${ZLIB_VERSION}.tar.gz -O /tmp/zlib-${ZLIB_VERSION}.tar.gz \

# wget --no-check-certificate --tries=5 https://www.openssl.org/source/openssl-${OPENSSL_VERSION}.tar.gz -O /tmp/openssl-${OPENSSL_VERSION}.tar.gz \

# wget --no-check-certificate --tries=5 https://openbsd.hk/pub/OpenBSD/OpenSSH/portable/openssh-${OPENSSH_VERSION}.tar.gz -O /tmp/openssh-${OPENSSH_VERSION}.tar.gz \

# wget --no-check-certificate --content-disposition --tries=5 https://packages.gitlab.com/gitlab/gitlab-ce/packages/ubuntu/xenial/gitlab-ce_${RELEASE_VERSION}_amd64.deb/download.deb -O /tmp/gitlab.deb && dpkg -i /tmp/gitlab.deb && rm /tmp/gitlab.deb

````
