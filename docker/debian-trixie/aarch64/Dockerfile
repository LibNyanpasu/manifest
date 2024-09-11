FROM debian:trixie
ENV DEBIAN_FRONTEND=noninteractive

# RUN rm -f /etc/apt/sources.list.d/debian.sources && \
#     rm -f /etc/apt/sources.list && \
#     echo "deb http://mirrors.nju.edu.cn/debian/ trixie main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list && \
#     echo "deb http://mirrors.nju.edu.cn/debian/ trixie-updates main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list && \
#     echo "deb http://mirrors.nju.edu.cn/debian/ trixie-backports main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list && \
#     echo "deb http://mirrors.nju.edu.cn/debian-security/ trixie-security main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list

RUN rm -f /etc/apt/sources.list.d/debian.sources && \
    rm -f /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian/ trixie-backports main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian-security/ trixie-security main contrib non-free non-free-firmware" | tee -a /etc/apt/sources.list

    RUN apt-get update && \
    apt-get install --assume-yes --no-install-recommends \
        gnupg2 \
        ca-certificates \
        g++-aarch64-linux-gnu \
        libc6-dev-arm64-cross \
        libclang-dev \
        build-essential \
        pkg-config \
        curl \
        wget \
        file && \
    rm -rf /var/lib/apt/lists/*

RUN dpkg --add-architecture arm64 && \
    apt-get update && apt-get install --assume-yes --no-install-recommends -f \
        libwebkit2gtk-4.1-dev:arm64 \
        libxdo-dev:arm64 \
        libssl-dev:arm64 \
        libgtk-3-dev:arm64 \
        libayatana-appindicator3-dev:arm64 \
        librsvg2-dev:arm64 \
        libatk1.0-dev:arm64 \
        libgdk-pixbuf-2.0-dev:arm64 \
        libcairo2-dev:arm64 \
        libpango1.0-dev:arm64 \
        libgtk-3-dev:arm64 \
        libsoup2.4-dev:arm64 && \
    rm -rf /var/lib/apt/lists/*

# Install NodeJs and pnpm
# RUN wget -qO- https://get.pnpm.io/install.sh | ENV="$HOME/.bashrc" SHELL="$(which bash)" bash - && \
#     pnpm env use --global lts

# ENV RUSTUP_DIST_SERVER="https://rsproxy.cn" \
#     RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"

# Install Rust
# RUN curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh -s -- -y --default-toolchain nightly --profile minimal
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain nightly --profile minimal
ENV PATH="/root/.cargo/bin:$PATH"
RUN rustup target add armv7-unknown-linux-gnueabi

# Set envs
ENV CARGO_TARGET_AARCH64_UNKNOWN_LINUX_GNU_LINKER=aarch64-linux-gnu-gcc \
    CC_aarch64_unknown_linux_gnu=aarch64-linux-gnu-gcc \
    CXX_aarch64_unknown_linux_gnu=aarch64-linux-gnu-g++ \
    BINDGEN_EXTRA_CLANG_ARGS_aarch64_unknown_linux_gnu="--sysroot=/usr/aarch64-linux-gnu" \
    PKG_CONFIG_PATH="/usr/lib/aarch64-linux-gnu/pkgconfig/:${PKG_CONFIG_PATH}" \
    PKG_CONFIG_ALLOW_CROSS=1

WORKDIR /app
