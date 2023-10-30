# DOCKER Readme

### Run PAPipe with Docker

**Install docker and get ready to load PAPipe docker image**

[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

```bash
curl -fsSL https://get.docker.com/ | sudo sh
sudo usermod -aG docker $USER 	# adding user to the “docker” group
```

**Load PAPipe docker image from the GitHub repository**

```jsx
glt clone https://github.com/nayoung9/PAPipe
cd PAPipe/Docker
docker load -i PAPipe.tar
```

**Create docker container mounting the tutorial data directory** 

```bash
docker run -it pap_docker:latest -v [absolute path of github/PAPipe/TEST/]:/RUN_DOCKER/
```

**Run PAPipe in the docker container** 

```bash
#on the docker container
mkdir /RUN_DOCKER/
cd /RUN_DOCKER/docker_test
python3 /PAPipe/bin/main.py  -P ./main_param.txt  -I main_input.txt -A main_sample.txt &> log
```