# Ubuntu Base images

## Available Tags

`lthn/build-c:ubuntu-16.04`, `lthn/build-c:ubuntu-18.04`,`lthn/build-c:ubuntu-20.04`,`lthn/build-c:ubuntu-22.04`

## Installed Packages

- all from `lthn/ubuntu:${VERSION}`
- make
- automake
- cmake
- g++-multilib
- libtool
- binutils
- bsdmainutils
- pkg-config
- python3
- patch
- bison 
- g++-arm-linux-gnueabihf
- binutils-arm-linux-gnueabihf
- g++-aarch64-linux-gnu
- binutils-aarch64-linux-gnu
- g++-powerpc64-linux-gnu
- binutils-powerpc64-linux-gnu
- g++-powerpc64le-linux-gnu
- binutils-powerpc64le-linux-gnu 
- g++-riscv64-linux-gnu
- binutils-riscv64-linux-gnu
- g++-s390x-linux-gnu
- binutils-s390x-linux-gnu

## Configuration Adjustments

```bash
echo '#!/bin/sh' > /usr/sbin/policy-rc.d
echo 'exit 101' >> /usr/sbin/policy-rc.d
chmod +x /usr/sbin/policy-rc.d
dpkg-divert --local --rename --add /sbin/initctl
cp -a /usr/sbin/policy-rc.d /sbin/initctl
sed -i 's/^exit.*/exit 0/' /sbin/initctl
echo 'force-unsafe-io' > /etc/dpkg/dpkg.cfg.d/docker-apt-speedup
echo 'DPkg::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' > /etc/apt/apt.conf.d/docker-clean
echo 'APT::Update::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' >> /etc/apt/apt.conf.d/docker-clean
echo 'Dir::Cache::pkgcache ""; Dir::Cache::srcpkgcache "";' >> /etc/apt/apt.conf.d/docker-clean
echo 'Acquire::Languages "none";' > /etc/apt/apt.conf.d/docker-no-languages
echo 'Acquire::GzipIndexes "true"; Acquire::CompressionTypes::Order:: "gz";' > /etc/apt/apt.conf.d/docker-gzip-indexes
echo 'Apt::AutoRemove::SuggestsImportant "false";' > /etc/apt/apt.conf.d/docker-autoremove-suggests
```
