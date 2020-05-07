FROM jupyter/base-notebook:notebook-6.0.3

USER root
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential wget git cmake tzdata \
    texlive-xetex texlive-fonts-recommended texlive-generic-recommended texlive-fonts-extra

RUN ln -s /opt/conda/bin/pip /usr/bin/pip3

WORKDIR /opt/setup/
RUN fix-permissions /opt/setup/ && fix-permissions /usr/local/bin/

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

COPY . .

# scanpy
RUN conda env create -f /opt/setup/scanpy/scanpy-1.4.6.yml && conda clean -a
RUN /opt/conda/envs/scanpy-1.4.6/bin/python -m ipykernel install --user --name scanpy-1.4.6 --display-name="scanpy-1.4.6"
RUN /opt/conda/envs/scanpy-1.4.6/bin/pip install git+https://github.com/JonathanShor/DoubletDetection.git@v2.5.2 && \
	/opt/conda/envs/scanpy-1.4.6/bin/pip install git+https://github.com/chriscainx/mnnpy.git@v0.1.9.4 && \
    # NetworkX
    /opt/conda/envs/scanpy-1.4.6/bin/pip install git+https://github.com/bhargavchippada/forceatlas2.git@v0.3.5

# scVI
RUN conda env create -f /opt/setup/scvi/scvi-0.6.4.yml && conda clean -a
RUN /opt/conda/envs/scvi-0.6.4/bin/python -m ipykernel install --user --name scvi-0.6.4 --display-name="scvi-0.6.4"

# palantir
RUN conda env create -f /opt/setup/palantir/palantir-0.2.5.yml && conda clean -a
RUN /opt/conda/envs/palantir-0.2.5/bin/python -m ipykernel install --user --name palantir-0.2.5 --display-name="palantir-0.2.5"
RUN ln -s /opt/conda/envs/palantir-0.2.5/bin/R /usr/local/bin/R && \
    /opt/conda/envs/palantir-0.2.5/bin/pip install git+https://github.com/jacoblevine/phenograph.git@7f4bc18699adb513a983ba183fdc7c989c219b85 && \
	/opt/conda/envs/palantir-0.2.5/bin/pip install git+https://github.com/dpeerlab/Palantir.git@v0.2.5 && \
	/opt/conda/envs/palantir-0.2.5/bin/pip install git+https://github.com/dpeerlab/Harmony.git@v0.1.3 && \
    rm /usr/local/bin/R

WORKDIR /home/jovyan/work