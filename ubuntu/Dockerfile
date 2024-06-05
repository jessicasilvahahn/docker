FROM ubuntu:20.04


#Set timezone
RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/Australia/Sydney /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

#Install QT6
RUN apt-get install -y \
    build-essential \
    libgl-dev \
    mesa-common-dev \
    libxcb-xinerama0-dev \
    libdbus-1-dev \
    libxkbcommon-x11-dev \
    libssl-dev \
    cmake \
    ninja-build \
    python3 \
    git

RUN git clone https://code.qt.io/qt/qt6.git /opt/qt6

WORKDIR /opt/qt6
RUN ./init-repository \
    && ./configure -prefix /opt/qt6-install -opensource -confirm-license -release -nomake examples -nomake tests \
    && make -j$(nproc) \
    && make install

RUN apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
