FROM ghcr.io/ponylang/ponyc-ci-x86-64-unknown-linux-ubuntu24.04-builder:20240425

ARG CROSS_TRIPLE=aarch64-unknown-linux-gnu
ARG CROSS_CC=aarch64-linux-gnu-gcc
ARG CROSS_CXX=aarch64-linux-gnu-g++
ARG CROSS_CFLAGS=
ARG CROSS_CXXFLAGS=
ARG CROSS_LDFLAGS=
ARG CROSS_BITS=64
ARG CROSS_LINKER=aarch64-linux-gnu-gcc
ARG CROSS_TUNE=cortex-a53

USER root

RUN curl -L --output gcc-linearo.tar.xz "https://releases.linaro.org/components/toolchain/binaries/7.5-2019.12/aarch64-linux-gnu/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu.tar.xz" \
 && tar xJf gcc-linearo.tar.xz -C /usr/local --strip 1 \
 && aarch64-linux-gnu-gcc --version \
 && rm gcc-linearo.tar.xz \
 && curl -L --output /usr/bin/qemu-aarch64-static https://github.com/multiarch/qemu-user-static/releases/download/v5.2.0-2/qemu-aarch64-static \
 && chmod +x /usr/bin/qemu-aarch64-static \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
  lldb \
 && rm -rf /var/lib/apt/lists/* \
 && apt-get -y autoremove --purge \
 && apt-get -y clean

RUN cmake --version

USER pony
WORKDIR /home/pony
