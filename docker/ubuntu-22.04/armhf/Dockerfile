# FROM ubuntu:jammy
# # cleanup sources.list and add arm64 architecture
# RUN rm -f /etc/apt/sources.list && \
#     echo "deb [arch=arm64] http://ports.ubuntu.com/ubuntu-ports/ jammy main restricted universe multiverse" | tee /etc/apt/sources.list && \
#     echo "deb [arch=arm64] http://ports.ubuntu.com/ubuntu-ports/ jammy-updates main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
#     echo "deb [arch=arm64] http://ports.ubuntu.com/ubuntu-ports/ jammy-security main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
#     echo "deb [arch=i386,amd64] http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
#     echo "deb [arch=i386,amd64] http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
#     echo "deb [arch=i386,amd64] http://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
#     dpkg --add-architecture arm64 && \
#     apt-get update && \
#     apt-get install -y \
#     autoconf \
#     automake \
#     binutils \
#     ca-certificates \
#     curl \
#     file \
#     gcc \
#     git \
#     libtool \
#     m4 \
#     make \
#     g++ \
#     unzip \
#     xz-utils \
#     gfortran \
#     libc6-dev \
#     libclang-dev \
#     pkg-config \
#     g++-aarch64-linux-gnu \
#     gfortran-aarch64-linux-gnu \
#     libc6-dev-arm64-cross \
#     libwebkit2gtk-4.1-dev:arm64 \
#     libxdo-dev:arm64 \
#     libayatana-appindicator3-dev:arm64 \
#     librsvg2-dev:arm64 \
#     libpango1.0-dev:arm64 \
#     libcairo2-dev:arm64 \
#     libatk1.0-dev:arm64 \
#     libsoup2.4-dev:arm64 \
#     libssl-dev:arm64


FROM ubuntu:jammy

# use ubuntu mirror
RUN rm -f /etc/apt/sources.list && \
    # echo "deb [arch=armhf] http://ports.ubuntu.com/ubuntu-ports/ jammy main restricted universe multiverse" | tee /etc/apt/sources.list && \
    # echo "deb [arch=armhf] http://ports.ubuntu.com/ubuntu-ports/ jammy-updates main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    # echo "deb [arch=armhf] http://ports.ubuntu.com/ubuntu-ports/ jammy-security main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    # echo "deb [arch=i386,amd64] http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    # echo "deb [arch=i386,amd64] http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    # echo "deb [arch=i386,amd64] http://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse" | tee -a /etc/apt/sources.list
    echo "deb [arch=armhf] http://mirrors.zju.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse" | tee /etc/apt/sources.list && \
    echo "deb [arch=armhf] http://mirrors.zju.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    echo "deb [arch=armhf] http://mirrors.zju.edu.cn/ubuntu-ports/ jammy-security main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    echo "deb [arch=i386,amd64] http://mirrors.zju.edu.cn/ubuntu/ jammy main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    echo "deb [arch=i386,amd64] http://mirrors.zju.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse" | tee -a /etc/apt/sources.list && \
    echo "deb [arch=i386,amd64] http://mirrors.zju.edu.cn/ubuntu/ jammy-security main restricted universe multiverse" | tee -a /etc/apt/sources.list
RUN apt-get update && \
    apt-get install --assume-yes --no-install-recommends \
    gnupg2 \
    ca-certificates \
    g++-arm-linux-gnueabihf \
    libc6-dev-armhf-cross \
    libclang-dev \
    build-essential \
    pkg-config \
    curl \
    wget \
    file

RUN dpkg --add-architecture armhf && \
    apt-get update && apt-get install --assume-yes --no-install-recommends -f \
    libwebkit2gtk-4.1-dev:armhf  \
    libxdo-dev:armhf  \
    libssl-dev:armhf  \
    libgtk-3-dev:armhf  \
    libayatana-appindicator3-dev:armhf  \
    librsvg2-dev:armhf \
    libatk1.0-dev:armhf \
    libgdk-pixbuf-2.0-dev:armhf \
    libcairo2-dev:armhf \
    libpango1.0-dev:armhf \
    libgtk-3-dev:armhf \
    libsoup2.4-dev:armhf

# Install NodeJs and pnpm
# RUN wget -qO- https://get.pnpm.io/install.sh | ENV="$HOME/.bashrc" SHELL="$(which bash)" bash - && \
#     pnpm env use --global lts

ENV RUSTUP_DIST_SERVER="https://rsproxy.cn" \
    RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh -s -- -y --default-toolchain nightly --profile minimal
# RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain nightly --profile minimal
ENV PATH="/root/.cargo/bin:$PATH"
RUN rustup target add armv7-unknown-linux-gnueabihf

# Set envs
# ENV CARGO_TARGET_AARCH64_UNKNOWN_LINUX_GNU_LINKER=aarch64-linux-gnu-gcc \
#     CC_aarch64_unknown_linux_gnu=aarch64-linux-gnu-gcc \
#     CXX_aarch64_unknown_linux_gnu=aarch64-linux-gnu-g++ \
#     BINDGEN_EXTRA_CLANG_ARGS_aarch64_unknown_linux_gnu="--sysroot=/usr/aarch64-linux-gnu" \
#     PKG_CONFIG_PATH="/usr/lib/aarch64-linux-gnu/pkgconfig/:${PKG_CONFIG_PATH}" \
#     PKG_CONFIG_ALLOW_CROSS=1

ENV CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABIHF_LINKER=arm-linux-gnueabihf-gcc \
    CC_armv7_unknown_linux_gnueabihf=arm-linux-gnueabihf-gcc \
    CXX_armv7_unknown_linux_gnueabihf=arm-linux-gnueabihf-g++ \
    BINDGEN_EXTRA_CLANG_ARGS_armv7_unknown_linux_gnueabihf="--sysroot=/usr/arm-linux-gnueabihf" \
    PKG_CONFIG_PATH="/usr/lib/arm-linux-gnueabihf/pkgconfig/:${PKG_CONFIG_PATH}" \
    PKG_CONFIG_ALLOW_CROSS=1

WORKDIR /app
