FROM buildpack-deps:bullseye

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        cmake \
        gcc-arm-none-eabi \ 
        libnewlib-arm-none-eabi \
        libstdc++-arm-none-eabi-newlib \
        libusb-1.0-0-dev \
        pkg-config; \
    rm -rf /var/lib/apt/lists/*

# Raspberry Pi Pico SDK installation
ENV PICO_SDK_PATH=/usr/share/pico_sdk
RUN set -ex; \
    git clone --depth 1 --branch 1.5.1 https://github.com/raspberrypi/pico-sdk $PICO_SDK_PATH; \
    cd $PICO_SDK_PATH; \
    git submodule update --init

# Picotool installation
RUN set -ex; \
    git clone --depth 1 --branch 1.1.2 https://github.com/raspberrypi/picotool.git /home/picotool; \
    cd /home/picotool; \
    mkdir build; \
    cd build; \
    cmake ..; \
    make; \
    cp /home/picotool/build/picotool /bin/picotool; \
    rm -rf /home/picotool

# Pico Extras installation
ENV PICO_EXTRAS_PATH=/usr/share/pico_extras
RUN set -ex; \
    git clone --depth 1 --branch sdk-1.5.1 https://github.com/raspberrypi/pico-extras.git $PICO_EXTRAS_PATH; \
    cd $PICO_EXTRAS_PATH; \
    git submodule update --init
