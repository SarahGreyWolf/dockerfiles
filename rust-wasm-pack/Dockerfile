# Based on jdrouet's wasm-pack image (https://github.com/jdrouet/dockerfiles/blob/main/rust-wasm-pack/Dockerfile)

FROM node:current-buster

# install tooling
RUN apt-get update \
    && apt-get install -y curl make \
    && rm -rf /var/lib/apt/lists/*

# install rust
ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates gcc libc6-dev \
    && curl -L --output rustup-init "https://static.rust-lang.org/rustup/dist/$(uname -m)-unknown-linux-gnu/rustup-init" \
    && chmod +x rustup-init \
    && ./rustup-init -y --no-modify-path --default-toolchain nightly \
    && rm rustup-init \
    && chmod -R a+w $RUSTUP_HOME $CARGO_HOME \
    && rustup --version \
    && cargo --version \
    && rustc --version \
    && rm -rf /var/lib/apt/lists/*

# install wasm-bindgen
RUN cargo install -f wasm-bindgen-cli

# install wasm-pack
RUN cargo install -f wasm-pack
