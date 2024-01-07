FROM ubuntu:22.04
RUN apt update && apt install -y libgtk-4-dev build-essential

RUN apt install -y curl

# Rust install
ENV RUST_HOME /usr/local/lib/rust
ENV RUSTUP_HOME ${RUST_HOME}/rustup
ENV CARGO_HOME ${RUST_HOME}/cargo
RUN mkdir /usr/local/lib/rust && chmod 0755 $RUST_HOME
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > ${RUST_HOME}/rustup.sh \
    && chmod +x ${RUST_HOME}/rustup.sh \
    && ${RUST_HOME}/rustup.sh -y --default-toolchain nightly --no-modify-path
ENV PATH $PATH:$CARGO_HOME/bin

# Rust build
RUN mkdir /work
WORKDIR /work
RUN cargo new hello-gtk
WORKDIR /work/hello-gtk
RUN cargo add gtk4@0.6.6 --rename gtk
COPY main.rs /work/hello-gtk/src/
RUN cargo build
