
FROM rust:1.31 as builder

RUN set -ex \
    && apt-get update \
    && apt-get --no-install-recommends --yes install \
    clang \
    cmake \
    git \
    libclang-dev \
    libncurses5 \
    libncursesw5 \
    llvm-dev

WORKDIR /usr/src

RUN git clone https://github.com/vault713/wallet713 \
    && cd wallet713 \
    && cargo build --release

LABEL vendor="vault713" \
    mw.713.version="1.0.1" \
    mw.713.release-date="02.02.2019" \
    maintainer="mi1b@protonmail.com"

FROM debian:9.4

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales openssl ca-certificates

RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && dpkg-reconfigure --frontend=noninteractive locales \
    && update-locale LANG=en_US.UTF-8
    
ENV LANG en_US.UTF-8

COPY --from=builder /usr/src/wallet713/target/release/wallet713 /usr/local/bin/wallet713

WORKDIR /
