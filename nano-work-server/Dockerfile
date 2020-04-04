FROM rust:1-slim-buster AS builder
# Install build dependencies
RUN apt-get update && \
    apt-get install -y git ocl-icd-opencl-dev && \
    git clone https://github.com/nanocurrency/nano-work-server.git && \
    cd nano-work-server && \
    cargo build --release && \
    rm -rf /var/lib/apt/lists/

FROM gcr.io/distroless/base-debian10

COPY --from=builder /lib/x86_64-linux-gnu/libgcc_s.so.1 /lib/x86_64-linux-gnu/libgcc_s.so.1
COPY --from=builder /usr/lib/x86_64-linux-gnu/libOpenCL.* /usr/lib/x86_64-linux-gnu/
COPY --from=builder /nano-work-server/target/release/nano-work-server /nano-work-server

ENTRYPOINT ["/nano-work-server"]