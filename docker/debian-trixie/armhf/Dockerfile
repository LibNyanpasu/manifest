FROM debian:trixie

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
    g++-arm-linux-gnueabihf \
    libc6-dev-armhf-cross \
    libclang-dev \
    build-essential \
    pkg-config \
    curl \
    wget \
    file && \
    rm -rf /var/lib/apt/lists/*

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
    libsoup2.4-dev:armhf && \
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
RUN rustup target add armv7-unknown-linux-gnueabihf

# Set envs
ENV CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABIHF_LINKER=arm-linux-gnueabihf-gcc \
    CC_armv7_unknown_linux_gnueabihf=arm-linux-gnueabihf-gcc \
    CXX_armv7_unknown_linux_gnueabihf=arm-linux-gnueabihf-g++ \
    BINDGEN_EXTRA_CLANG_ARGS_armv7_unknown_linux_gnueabihf="--sysroot=/usr/arm-linux-gnueabihf" \
    PKG_CONFIG_PATH="/usr/lib/arm-linux-gnueabihf/pkgconfig/:${PKG_CONFIG_PATH}" \
    PKG_CONFIG_ALLOW_CROSS=1

WORKDIR /app
