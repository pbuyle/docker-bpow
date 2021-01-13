# Banano Vanity

Docker container running [banano-vanity](https://github.com/BananoCoin/banano-vanity).

The `latest` image uses [distroless](https://github.com/GoogleContainerTools/distroless), the final image weights ~25Mb. Support for GPUs is unlikely with this image.

The `nvidia` image uses [nvidia's OpenCL base image](https://hub.docker.com/r/nvidia/opencl/), the final image weights ~90Mb. It provides support for both CPU and GPU with [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker) which should be installed on the host system.

## Usage

    docker run --rm pbuyle/banano-vanity 3anano

    docker run --rm --gpus all pbuyle/banano-vanity:nvidia --gpu 3anano