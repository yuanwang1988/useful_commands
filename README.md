# Useful Commands


## Start a local docker backend for Colab
The following instructions is needed to allow the Colab to connect to a docker based backend.

**Step 1:** Run the following command in terminal
```console
docker run --gpus all -it -p 8888:8888 tensorflow/tensorflow:latest-gpu-jupyter jupyter notebook --notebook-dir=/tf --ip 0.0.0.0 --no-browser --allow-root --NotebookApp.allow_origin='https://colab.research.google.com'
```

**Step 2:** In Colab, connect to local run time. Copy the URL from terminal. Replace IP address with ```localhost```.

## Installing NVIDIA Container Toolkit for Docker
The following instructions is needed to resolve problems with installing NVIDIA Container Toolkit for Docker on Pop OS 20.04.

**Step 1:** Run the following command in terminal:
```console
distribution=ubuntu20.04 && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```

**Step 2:** Edit the following file to give higher priority to nvidia repos
```console
sudo vim /etc/apt/preferences.d/pop-default-settings
```
Add the following

```console
Package: *
Pin: origin nvidia.github.io
Pin-Priority: 1002
```

**Step 3:** Install docker
```console
sudo apt update
sudo apt install nvidia-docker2
sudo systemctl restart docker
```

**Step 4:** Test installation by running:
```console
sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
```

## Run Docker without sudo
**Step 1:** Run the following commands
```console
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker 
```

**Step 2:** Test by running
```console
docker run hello-world
```

## Fix IPython Autocomplete Issue
IPython Notebook often fail due to Jedi autocompletion. 

Add the following to the Colab
```python
%config Completer.use_jedi = False
```
