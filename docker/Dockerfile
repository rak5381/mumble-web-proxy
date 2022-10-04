FROM rust:1.64-alpine AS build

RUN apk add --no-cache \
    clang-libs \
    curl \
    libc-dev \
    libnice-dev \
    openssl-dev \
    ;
WORKDIR /src
COPY Cargo.toml Cargo.lock ./
COPY src ./src
RUN echo -e '\n[dependencies."async-trait"]\ndefault-features = false' >> Cargo.toml
RUN RUSTFLAGS="-C target-feature=-crt-static" cargo install --path .

FROM alpine

RUN apk add --no-cache \
    bash \
    libgcc \
    libnice \
    ;
COPY --from=build /usr/local/cargo/bin/mumble-web-proxy /mumble-web-proxy
COPY docker/entrypoint.sh /entrypoint.sh

ENV MWP_LISTEN_WS=64737
ENV MWP_SERVER=mumble-server:64738
ENV MWP_ACCEPT_INVALID_CERTIFICATE=
ENV MWP_ICE_PORT_MIN=
ENV MWP_ICE_PORT_MAX=
ENV MWP_ICE_IPV4=
ENV MWP_ICE_IPV6=

CMD ["/entrypoint.sh"]
USER 1000
EXPOSE 64737
