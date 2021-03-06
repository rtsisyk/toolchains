FROM mato/rumprun-toolchain-hw-x86_64
MAINTAINER Roman Tsisyk <roman@tarantool.org>

RUN sudo apt-get update && sudo apt-get install -y wget cmake

# Install LibreSSL
RUN wget http://ftp.openbsd.org/pub/OpenBSD/LibreSSL/libressl-2.4.2.tar.gz && \
    tar xvf libressl-*.tar.* && cd libressl-*/ && \
    ./configure \
        --prefix=/usr/local/rumprun-x86_64 \
        --build=x86_64-linux-gnu \
        --host=x86_64-rumprun-netbsd \
        --enable-shared=no && \
    make -j && sudo make install && \
    cd .. && rm -rf libressl-* && \
    sudo rm -rf /usr/share/{man,info,doc}/

# Install ncurses
RUN wget http://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.0.tar.gz && \
    tar xvf ncurses-*.tar.* && cd ncurses-*/ && \
    ./configure \
        --prefix=/usr/local/rumprun-x86_64 \
        --includedir=/usr/local/rumprun-x86_64/include \
        --build=x86_64-linux-gnu \
        --host=x86_64-rumprun-netbsd \
        --without-ada \
        --disable-termcap \
        --disable-rpath-hack \
        --without-cxx \
        --without-cxx-binding \
        --without-shared && \
    make -j && sudo make install && \
    cd .. && rm -rf ncurses-* && \
    sudo rm -rf /usr/share/{man,info,doc}/

# Install libreadline
RUN wget http://ftp.gnu.org/gnu/readline/readline-7.0.tar.gz && \
    tar xvf readline-*.tar.* && cd readline-*/ && \
    SHLIB_XLDFLAGS="" ./configure \
        --prefix=/usr/local/rumprun-x86_64 \
        --build=x86_64-linux-gnu \
        --host=x86_64-rumprun-netbsd \
        --enable-static \
        --disable-shared && \
    make -j && sudo make install && \
    cd .. && rm -rf readline-* && \
    sudo rm -rf /usr/share/{man,info,doc}/

# Add patched CMake toolchain configuration
ADD x86_64-rumprun-netbsd-toolchain.cmake /usr/local/rumprun-x86_64/share/x86_64-rumprun-netbsd-toolchain.cmake
ADD x86_64-rumprun-netbsd-cmake /usr/local/bin
