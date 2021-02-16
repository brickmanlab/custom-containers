FROM jupyter/base-notebook:notebook-6.1.4

USER root
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential wget git cmake tzdata

RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    # other
    jupyter labextension install @jupyterlab/toc --no-build && \
    jupyter labextension install @aquirdturtle/collapsible_headings --no-build && \
    jupyter labextension install jupyterlab-execute-time --no-build && \
    # code formater
    jupyter labextension install @ryantam626/jupyterlab_code_formatter && \
    pip install jupyterlab_code_formatter black yapf autopep8 isort && \
    jupyter serverextension enable --py jupyterlab_code_formatter && \
    # build
    jupyter lab build && jupyter lab clean

COPY . /opt/setup/
RUN mkdir -p ~/.jupyter/lab/user-settings/@jupyterlab/notebook-extension/ && \
    mv /opt/setup/tracker.jupyterlab-settings ~/.jupyter/lab/user-settings/@jupyterlab/notebook-extension/

RUN chown -R jovyan:users /opt/setup/

USER jovyan

WORKDIR /home/jovyan/work