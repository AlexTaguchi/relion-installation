# relion-installation
Installation guide for the NVIDIA [RELION 5.0](https://www3.mrc-lmb.cam.ac.uk/relion) container with GPU acceleration

---

## 📁 Contents

- [Overview](#overview)
- [Local Mac Setup](#local-mac-setup)
- [Remote Ubuntu Setup](#remote-ubuntu-setup)
- [Running the Container with GUI](#running-the-container-with-gui)
- [Running RELION GUI](#running-relion-gui)
- [Tips](#tips)

---

## 📌 Overview

We will use:
- Docker with **NVIDIA GPU support**
- **X11 GUI forwarding** for running RELION interactively

---

## 💻 Local Mac Setup

1. **Install XQuartz**  
   [https://www.xquartz.org](https://www.xquartz.org)

2. **Run XQuartz**  
   *Applications > Utilities > XQuartz*

---

## 🖥️ Remote GPU Server Setup

1. **SSH with X11 forwarding**  
   ```bash
   ssh -X your_username@your_remote_server

2. **Install Docker**  
   ```bash
   sudo apt update
   sudo apt install -y docker.io

3. **Install NVIDIA Container Toolkit**  
   [https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)

5. **Pull the RELION 5.0 Docker image**  
   ```bash
   docker pull nvcr.io/hpc/relion:5.0.0
 
6. **Launch RELION container**  
   ```bash
   docker run -it --rm \
   --runtime=nvidia \
   --gpus all \
   --ipc=host \
   --net=host \
   -e DISPLAY=$DISPLAY \
   -v /tmp/.X11-unix:/tmp/.X11-unix \
   -v $HOME/.Xauthority:/root/.Xauthority \
   -v $PWD:/host_pwd \
   -w /host_pwd \
   nvcr.io/hpc/relion:5.0.0

7. **Launch RELION**  
   ```bash
   relion &
   
