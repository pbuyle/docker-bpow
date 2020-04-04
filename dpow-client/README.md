# Nano DPoW Client

Dokcer container for [Nano DPoW](https://github.com/guilhermelawless/nano-dpow) client.

## Usage

With [docker-compose](https://docs.docker.com/compose/):
```
version: "3.7"

services:
  nano-work-server:
    image: pbuyle/nano-work-server
    command: -c 8 -l 0.0.0.0:7000
    
  dpow-client:
    image: pbuyle/dpow-client
    depends_on:
      - nano-work-server
    command: --payout nano_1ii1irpoopmocgu69n56a9rdj47mu9wyar7pdr478h73juw59tuthojsbub4 --worker_uri nano-work-server:7000
```