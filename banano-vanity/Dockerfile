FROM rust:1-slim-buster AS builder
# Install build dependencies
RUN apt-get update && \
    apt-get install -y git ocl-icd-opencl-dev build-essential && \
    git clone https://github.com/BananoCoin/banano-vanity.git && \
    cd banano-vanity && \
    cargo build --release && \
    rm -rf /var/lib/apt/lists/

FROM gcr.io/distroless/base-debian10

COPY --from=builder /lib/x86_64-linux-gnu/libgcc_s.so.1 /lib/x86_64-linux-gnu/libgcc_s.so.1
COPY --from=builder /usr/lib/x86_64-linux-gnu/libOpenCL.* /usr/lib/x86_64-linux-gnu/
COPY --from=builder banano-vanity/target/release/banano-vanity /banano-vanity

ENTRYPOINT ["/banano-vanity"]