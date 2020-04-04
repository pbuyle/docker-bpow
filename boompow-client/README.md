# BoomPow Client

Dokcer container for [BooomPow Client](https://github.com/BananoCoin/boompow).

## Usage

With [docker-compose](https://docs.docker.com/compose/):
```
version: "3.7"

services:
  nano-work-server:
    image: pbuyle/nano-work-server
    command: -c 8 -l 0.0.0.0:7000
    
  boompow-client:
    image: pbuyle/bpow-client
    depends_on:
      - nano-work-server
    command: --limit-logging --async_mode --payout ban_3se931ts5w1xmn988jeztyz8nh35nfp6bwc33xgxom3hib8cex4zxhsom9fz --worker_uri nano-work-server:7000
```