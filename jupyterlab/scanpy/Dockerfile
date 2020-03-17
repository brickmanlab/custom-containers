FROM jupyter/base-notebook:notebook-6.0.0

USER root
RUN apt-get update && apt-get install -y build-essential wget git cmake

# Link pip -> pip3
RUN ln -s /opt/conda/bin/pip /usr/bin/pip3

WORKDIR /opt/setup/
RUN fix-permissions /opt/setup/

USER jovyan

# Copy all environments
COPY . .

# Scanpy Setup
RUN conda env create -f /opt/setup/environment.yml && conda clean --all -f -y
ENV PATH /opt/conda/envs/scanpy-env/bin:$PATH
ENV CONDA_DEFAULT_ENV scanpy-env
RUN python -m ipykernel install --user --name scanpy-env --display-name="Scanpy setup" && \
	jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
	jupyter labextension install @jupyter-widgets/jupyterlab-manager@^1.0.1 --no-build && \
    jupyter labextension install jupyterlab_bokeh@1.0.0 --no-build && \
	jupyter labextension install jupyterlab-plotly@1.5.3 --no-build && \
	jupyter labextension install @jupyterlab/toc && \
	jupyter labextension install plotlywidget@1.5.3 --no-build && \
    jupyter lab build

RUN pip install fa2 && \
	# Palantir Setup
	pip install git+https://github.com/jacoblevine/phenograph.git@7f4bc18699adb513a983ba183fdc7c989c219b85 && \
	pip install git+https://github.com/dpeerlab/Palantir.git@v0.2.1 && \
	pip install git+https://github.com/JonathanShor/DoubletDetection.git@v2.5.2 && \
	pip install git+https://github.com/chriscainx/mnnpy.git@v0.1.9.4

WORKDIR /home/jovyan/work
