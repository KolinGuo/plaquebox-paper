FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04
#FROM pytorch/pytorch:1.1.0-cuda10.0-cudnn7.5-devel

RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential \
  cmake \
  wget \
  git \
  curl \
  ca-certificates \
  libjpeg-dev \
  libpng-dev \
  vim \
  apt-utils \
  software-properties-common \
  && rm -rf /var/lib/apt/lists/*

######################################
# SECTION 1: Python 3.6 packages     #
######################################
RUN add-apt-repository ppa:jonathonf/python-3.6 && apt-get update \
  && apt-get install -y python3.6 python3.6-dev python3.6-venv
RUN wget https://bootstrap.pypa.io/get-pip.py && python3.6 get-pip.py
RUN ln -sf /usr/bin/python3.6 /usr/bin/python3

RUN apt-get update && apt-get install -y --no-install-recommends libvips libvips-dev
RUN apt-get -y upgrade

RUN pip3.6 install pip --upgrade
RUN pip3.6 install -U numpy cython ipython jupyter matplotlib pandas scikit-learn \
  scikit-image scipy tqdm
#RUN pip3.6 install https://download.pytorch.org/whl/cu100/torch-1.1.0-cp36-cp36m-linux_x86_64.whl
# Use previous version to read trained model
RUN pip3.6 install torch==0.3.1 -f https://download.pytorch.org/whl/cu100/stable
#RUN pip3.6 install https://download.pytorch.org/whl/cu100/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl
RUN pip3.6 install torchvision==0.2.1
RUN pip3.6 install pyvips

######################################
# SECTION 2: OpenCV packages         #
######################################
#RUN mkdir -p /tmp/install/
#ADD ./install/opencv3 /tmp/install/opencv3
#RUN chmod +x /tmp/install/opencv3/install.sh && /tmp/install/opencv3/install.sh /usr/local
RUN pip3.6 install -U opencv-python==3.4.5.20

######################################
# SECTION 3: Additional Utilities    #
######################################
RUN echo "export PATH=$PATH:~/.local/bin/" >> /root/.bashrc
RUN apt update && apt -y upgrade

WORKDIR /root

######################################
# SECTION 4: Add running instruction #
######################################
RUN echo "echo -e \"\n\"" >> /root/.bashrc
RUN echo "echo -e \"################################################################################\n\"" >> /root/.bashrc
RUN echo "echo -e \"\tCommand to enter repository:\n\t\tcd /root/plaquebox-paper && jupyter notebook --no-browser --ip=0.0.0.0 --allow-root --port=9000 &\n\"" >> /root/.bashrc
RUN echo "echo -e \"################################################################################\n\"" >> /root/.bashrc
