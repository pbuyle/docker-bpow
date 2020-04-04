FROM python:3.7-alpine AS builder
ENV PYTHONUNBUFFERED 1

RUN apk --update upgrade && \
    apk add --update build-base && \
    rm -rf /var/cache/apk/* && \
    wget https://github.com/BananoCoin/boompow/releases/download/v2.0.2/bpow-client-v202.zip -O - | unzip -d / - && \
    mkdir /wheels && \
    cd /wheels && \
    pip wheel --no-cache-dir -r /bpow-client/requirements.txt && \
    rm -rf /bpow-client/bin

FROM python:3.7-alpine
ENV PYTHONUNBUFFERED 1

COPY --from=builder /wheels /wheels
COPY --from=builder /bpow-client /bpow-client

WORKDIR /bpow-client
RUN pip install --no-cache-dir -r /bpow-client/requirements.txt -f /wheels && \
    rm -rf /wheels

ENTRYPOINT ["python3", "/bpow-client/bpow_client.py"]