FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    cmake \
    gcc \
    libc6-dev \
    make \
    pkg-config

COPY xargo.sh /
RUN bash /xargo.sh

COPY openssl.sh qemu.sh /
RUN apt-get install -y --no-install-recommends \
    g++-mips64el-linux-gnuabi64 \
    libc6-dev-mips64el-cross && \
    bash /openssl.sh linux64-mips64 mips64el-linux-gnuabi64- && \
    bash /qemu.sh mips64el

ENV CARGO_TARGET_MIPS64EL_UNKNOWN_LINUX_GNUABI64_LINKER=mips64el-linux-gnuabi64-gcc \
    CARGO_TARGET_MIPS64EL_UNKNOWN_LINUX_GNUABI64_RUNNER=qemu-mips64el \
    CC_mips64el_unknown_linux_gnuabi64=mips64el-linux-gnuabi64-gcc \
    CXX_mips64el_unknown_linux_gnuabi64=mips64el-linux-gnuabi64-g++ \
    OPENSSL_DIR=/openssl \
    OPENSSL_INCLUDE_DIR=/openssl/include \
    OPENSSL_LIB_DIR=/openssl/lib \
    QEMU_LD_PREFIX=/usr/mips64el-linux-gnuabi64 \
    RUST_TEST_THREADS=1
