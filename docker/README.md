# mumble-web-proxy OCI image

This directory provides files to build a mumble-web-proxy OCI image.
The image is based on Alpine Linux and is less than 30 MiB in size.
One can use [Docker](https://www.docker.com/) in order to build the image,
as follows in the main repository directory:

```
docker build -t mumble-web-proxy -f docker/Dockerfile .
```
