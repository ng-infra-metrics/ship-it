FROM buildpack-deps:stretch

ENV CARGO_HOME=/opt/cargo

ENV PATH=$CARGO_HOME/bin:$PATH

RUN apt-get update && apt-get install -y libssl-dev pkg-config cmake zlib1g-dev

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y  --default-toolchain none

RUN rustup toolchain add stable beta nightly

RUN rustup component add --toolchain nightly rustfmt-preview

RUN cargo +nightly install clippy

RUN cargo +stable install cargo-tarpaulin

