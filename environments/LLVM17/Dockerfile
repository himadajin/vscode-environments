FROM buildpack-deps:bullseye

RUN apt-get update && apt-get install -y \
    lsb-release \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

# install LLVM
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - \
    && apt-add-repository "deb http://apt.llvm.org/bullseye/ llvm-toolchain-bullseye-17 main" \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    llvm-17 \
    llvm-17-dev \
    clang-17 \
    clang-format-17 \
    && rm -rf /var/lib/apt/lists/*

# setup alternatives
COPY setup-alternatives.sh /tmp/setup-alternatives.sh
RUN chmod +x /tmp/setup-alternatives.sh \
    && /tmp/setup-alternatives.sh \
    && rm /tmp/setup-alternatives.sh
