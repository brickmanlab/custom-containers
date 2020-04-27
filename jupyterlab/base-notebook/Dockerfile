FROM jupyter/base-notebook:notebook-6.0.0

USER root
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential wget git cmake tzdata \
    texlive-xetex texlive-fonts-recommended texlive-generic-recommended texlive-fonts-extra

RUN ln -s /opt/conda/bin/pip /usr/bin/pip3

WORKDIR /opt/setup/
RUN fix-permissions /opt/setup/

USER jovyan

RUN conda install --quiet --yes \
    'conda-forge::ipywidgets=7.5.*' \
    'conda-forge::nodejs' && \
    conda clean --all -y && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    # visualization
    jupyter labextension install @bokeh/jupyter_bokeh --no-build && \
    jupyter labextension install jupyter-matplotlib --no-build && \
    jupyter labextension install jupyterlab-plotly --no-build && \
    jupyter labextension install plotlywidget --no-build && \
    jupyter labextension install jupyter-cytoscape --no-build && \
    # other
    jupyter labextension install @jupyterlab/toc --no-build && \
    jupyter labextension install @aquirdturtle/collapsible_headings --no-build && \
    # build
    jupyter lab build && \
    jupyter lab clean && \
    npm cache clean --force && \
    rm -rf /home/$NB_USER/.cache/yarn && \
    rm -rf /home/$NB_USER/.node-gyp && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/jovyan
