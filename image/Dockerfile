FROM continuumio/miniconda:4.7.12

COPY environment.yml /app/
RUN conda env create -f /app/environment.yml && conda clean -a

ENV PATH /opt/conda/envs/image-1.1/bin:$PATH

RUN conda env export --name image-1.1 > /app/image-1.1.yml

# Download app and data
WORKDIR /image
RUN wget http://bioinformatik.sdu.dk/solexa/webshare/IMAGE/IMAGE_v1.1.tar.gz \
    && tar -xvf IMAGE_v1.1.tar.gz --strip 1 \
    && wget http://bioinformatik.sdu.dk/solexa/webshare/IMAGE/IMAGE_Data.tar.gz \
    && tar -xvf IMAGE_Data.tar.gz \
    # cleanup
    && rm IMAGE_v1.1.tar.gz IMAGE_Data.tar.gz
