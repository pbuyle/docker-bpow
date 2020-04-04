FROM python:3.7-alpine AS builder
ENV PYTHONUNBUFFERED 1

RUN apk --update upgrade && \
    apk add --update build-base git && \
    rm -rf /var/cache/apk/* && \
    git clone https://github.com/guilhermelawless/nano-dpow.git /nano-dpow && \
    mkdir /wheels && \
    cd /wheels && \
    pip wheel --no-cache-dir -r /nano-dpow/client/requirements.txt && \
    rm -rf /nano-dpow/client/bin

FROM python:3.7-alpine
ENV PYTHONUNBUFFERED 1

COPY --from=builder /wheels /wheels
COPY --from=builder /nano-dpow/client /dpow-client

WORKDIR /dpow-client
RUN pip install --no-cache-dir -r /dpow-client/requirements.txt -f /wheels && \
    rm -rf /wheels

ENTRYPOINT ["python3", "/dpow-client/dpow_client.py"]