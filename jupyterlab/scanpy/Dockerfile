FROM brickmanlab/base-notebook:6.0.0

USER jovyan

# Copy all environments
COPY . .

# Scanpy Setup
RUN conda env create -f /opt/setup/environment.yml && conda clean --all -f -y
ENV PATH /opt/conda/envs/scanpy-env/bin:$PATH
ENV CONDA_DEFAULT_ENV scanpy-env
RUN python -m ipykernel install --user --name scanpy-env --display-name="Scanpy setup"

RUN pip install git+https://github.com/bhargavchippada/forceatlas2.git@v0.3.5 && \
	# Palantir Setup
	pip install git+https://github.com/jacoblevine/phenograph.git@7f4bc18699adb513a983ba183fdc7c989c219b85 && \
	pip install git+https://github.com/dpeerlab/Palantir.git@v0.2.1 && \
	pip install git+https://github.com/dpeerlab/Harmony.git@531b4e8a517c7b06351630596d2d262fbb8cb011 && \
	pip install git+https://github.com/JonathanShor/DoubletDetection.git@v2.5.2 && \
	pip install git+https://github.com/chriscainx/mnnpy.git@v0.1.9.4

WORKDIR /home/jovyan/work
