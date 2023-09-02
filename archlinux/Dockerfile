FROM archlinux:base-devel
ARG TOOLCHAIN_PACKAGE
ARG CMAKE_GENERATOR_PACKAGE
ARG CMAKE_GENERATOR
ARG CMAKE_C_COMPILER
ARG CMAKE_CXX_COMPILER
WORKDIR /work/mold
RUN true && \
    pacman -Syu --noconfirm git cmake util-linux "$TOOLCHAIN_PACKAGE" "$CMAKE_GENERATOR_PACKAGE" && \
    git clone --depth=1 https://github.com/rui314/mold . && \
    git rev-parse HEAD && \
    mkdir -p build && \
    cd ./build && \
    cmake \
      -G"$CMAKE_GENERATOR" \
      -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_COMPILER="$CMAKE_C_COMPILER" \
      -DCMAKE_CXX_COMPILER="$CMAKE_CXX_COMPILER" \
      .. && \
    MAKEFLAGS="-j$(nproc)" cmake --build . && \
    ./mold --version && \
    true
