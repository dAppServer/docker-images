ARG VERSION=20.04
FROM ubuntu:${VERSION}

ENV DEBIAN_FRONTEND=noninteractive

# Add Image Authors
LABEL org.opencontainers.image.authors="snider@lethean.io"

RUN set -xe \
    && echo '#!/bin/sh' > /usr/sbin/policy-rc.d\
    && echo 'exit 101' >> /usr/sbin/policy-rc.d\
    && chmod +x /usr/sbin/policy-rc.d\
    && dpkg-divert --local --rename --add /sbin/initctl\
    && cp -a /usr/sbin/policy-rc.d /sbin/initctl\
    && sed -i 's/^exit.*/exit 0/' /sbin/initctl\
    && echo 'force-unsafe-io' > /etc/dpkg/dpkg.cfg.d/docker-apt-speedup\
    && echo 'DPkg::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' > /etc/apt/apt.conf.d/docker-clean\
    && echo 'APT::Update::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' >> /etc/apt/apt.conf.d/docker-clean\
    && echo 'Dir::Cache::pkgcache ""; Dir::Cache::srcpkgcache "";' >> /etc/apt/apt.conf.d/docker-clean\
    && echo 'Acquire::Languages "none";' > /etc/apt/apt.conf.d/docker-no-languages\
    && echo 'Acquire::GzipIndexes "true"; Acquire::CompressionTypes::Order:: "gz";' > /etc/apt/apt.conf.d/docker-gzip-indexes\
    && echo 'Apt::AutoRemove::SuggestsImportant "false";' > /etc/apt/apt.conf.d/docker-autoremove-suggests

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y build-essential curl git wget libssl-dev liblzo2-dev libpam0g-dev build-essential autoconf \
                      liblz4-dev libtool pkg-config libcap-ng-dev

# Make Lethean bin dir
RUN mkdir -p /home/lthn/bin
