FROM tensorflow/tensorflow:1.13.1-gpu-py3-jupyter

RUN apt-get update && apt-get install -y \
  apt-transport-https \
  libblas-dev liblapack-dev libatlas-base-dev \
  gfortran \
  build-essential \
  cmake \
  git \
  wget \
  unzip \
  yasm \
  pkg-config \
  libswscale-dev \
  libtbb2 \
  libjpeg-dev \
  libpng-dev \
  libtiff-dev \
  libavformat-dev \
  libpq-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

RUN pip --no-cache-dir install \
    ipykernel scipy scikit-image jupyter matplotlib pandas numpy opencv-python && \
    python -m ipykernel.kernelspec 

COPY ./config/jupyter_notebook_config.py /root/.jupyter/

# Jupyter has issues with being run directly:
# https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY ./config/run_jupyter.sh /

# Jupyter
EXPOSE 8888

WORKDIR /
VOLUME "/notebooks"
WORKDIR "/notebooks"

CMD ["/run_jupyter.sh"]
