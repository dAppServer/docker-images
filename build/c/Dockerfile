ARG VERSION=ubuntu:20.04
FROM lthn/${VERSION}

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y make automake cmake curl g++-multilib libtool binutils bsdmainutils pkg-config python3 patch bison \
    g++-arm-linux-gnueabihf binutils-arm-linux-gnueabihf g++-aarch64-linux-gnu binutils-aarch64-linux-gnu \
    g++-powerpc64-linux-gnu binutils-powerpc64-linux-gnu g++-powerpc64le-linux-gnu binutils-powerpc64le-linux-gnu \
    g++-riscv64-linux-gnu binutils-riscv64-linux-gnu g++-s390x-linux-gnu binutils-s390x-linux-gnu


