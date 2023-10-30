# DOCKER Readme

### Run PAPipe with Docker

**Install docker and get ready to load PAPipe docker image**

[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

```bash
curl -fsSL https://get.docker.com/ | sudo sh
sudo usermod -aG docker $USER 	# adding user to the “docker” group
```

**Git clone PAPipe repository**

```bash
glt clone https://github.com/nayoung9/PAPipe
```

**Download Tutorial data and get ready to run** 

```bash
cd PAPipe/TEST/
wget http://bioinfo.konkuk.ac.kr/practice/nayoung/PAPipe/test_data.tar.gz
tar -zxvf test_data.tar.gz
```

(1) **Build PAPipe docker image from the GitHub repository**

```bash
cd PAPipe/Docker/
docker build -t pap_docker:latest ./ &> docker.build.log

#Check if the image load well 
docker image ls 
```

(2) **Or you can download .tar file and load the image** 

```bash
wget http://bioinfo.konkuk.ac.kr/practice/nayoung/PAPipe/PAPipe.tar
docker load -i ./PAPipe.tar

#Check if the image load well 
docker image ls 
```

**Create docker container mounting the tutorial data directory** 

```bash
cd PAPipe/TEST/
docker run -v [absolute path of .../PAPipe/TEST/]:/RUN_DOCKER/  -it pap_docker:latest
```

**Run PAPipe in the docker container** 

```bash
#on the docker container
cd /RUN_DOCKER/docker_test
python3 /PAPipe/bin/main.py  -P ./main_param.txt  -I main_input.txt -A main_sample.txt &> log
```
