# IMAGE 1.1

## Reproduce

To reproduce the original paper:

1. Download the test data

```bash
wget http://bioinformatik.sdu.dk/solexa/webshare/IMAGE/IMAGE_Data.tar.gz && \
tar -xvf IMAGE_Data.tar.gz && \
rm IMAGE_Data.tar.gz
```

2. Mount `Data` into container

```bash
docker run -it -v ~/Downloads/Data:/image/Data brickmanlab/image:1.1
```
