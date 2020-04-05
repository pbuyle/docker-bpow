# Nano work server

Docker container running [nano-work-server](https://github.com/nanocurrency/nano-work-server).

The `latest` image uses [distroless](https://github.com/GoogleContainerTools/distroless), the final image weights ~25Mb. Support for GPUs is unlikely with this image.

The `nvidia` image uses [nvidia's OpenCL base image](https://hub.docker.com/r/nvidia/opencl/), the final image weights ~90Mb. It provides support for both CPU and GPU with [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker) which should be installed on the host system.

## Usage

    docker run --rm -p 127.0.0.1:7000:7000/tcp pbuyle/nano-work-server --cpu-threads 4 --listen-address 0.0.0.0:7000

    docker run --rm --gpus all -p 127.0.0.1:7000:7000/tcp pbuyle/nano-work-server:nvidia --gpu 0:0 --listen-address 0.0.0.0:7000