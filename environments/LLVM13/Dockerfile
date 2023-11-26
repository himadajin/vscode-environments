FROM buildpack-deps:bullseye

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    gcc \
    make \
    git \
    binutils \
    libc6-dev \
    software-properties-common \
    lsb-release \
    && rm -rf /var/lib/apt/lists/*

# install LLVM
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - \
    && apt-add-repository "deb http://apt.llvm.org/bullseye/ llvm-toolchain-bullseye-13 main" \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    llvm-13 \
    llvm-13-dev \
    clang-13 \
    && rm -rf /var/lib/apt/lists/*

# setup alternatives
COPY setup-alternatives.sh /tmp/setup-alternatives.sh
RUN chmod +x /tmp/setup-alternatives.sh \
    && /tmp/setup-alternatives.sh \
    && rm /tmp/setup-alternatives.sh