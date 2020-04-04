FROM rust:1-slim-buster AS builder
# Install build dependencies
RUN apt-get update && \
    apt-get install -y git ocl-icd-opencl-dev && \
    git clone https://github.com/nanocurrency/nano-work-server.git && \
    cd nano-work-server && \
    cargo build --release && \
    rm -rf /var/lib/apt/lists/

FROM debian:buster-slim

RUN apt-get update && \
    apt-get install -y ocl-icd-libopencl1 && \
    rm -rf /var/lib/apt/lists/

COPY --from=builder /nano-work-server/target/release/nano-work-server /nano-work-server

ENTRYPOINT ["/nano-work-server"]