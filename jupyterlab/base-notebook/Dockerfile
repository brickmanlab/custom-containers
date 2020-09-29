FROM jupyter/base-notebook:notebook-6.1.4

USER root
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential wget git cmake tzdata

RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    # other
    jupyter labextension install @jupyterlab/toc --no-build && \
    jupyter labextension install @aquirdturtle/collapsible_headings --no-build && \
    # build
    jupyter lab build && jupyter lab clean

COPY . /opt/setup/

RUN chown -R jovyan:users /opt/setup/

USER jovyan

# scanpy
RUN conda env create -f /opt/setup/scanpy/scanpy-1.6.0.yml && conda clean -a
RUN /opt/conda/envs/scanpy-1.6.0/bin/python -m ipykernel install --user --name scanpy-1.6.0 --display-name="scanpy-1.6.0"

WORKDIR /home/jovyan/work