---
layout: post
title: ubuntu nvidia-docker 설치하기.
modified:
categories: etc
excerpt:
tags: [ubuntu]
image:
  feature:
---

# nvidia-docker 설치하기

# 순서
- 중요하다. 순서.
- 이거잘못되서 몇번을 우분투를 다시깔았는지 모르겠따. (*시무룩*)

1. 그래픽카드 driver 설치하기
2. cuda, cudnn 설치하기
3. 도커 engine 설치하기
4. nvidia-docker 설치하기.

# 1. Nvidia 그래픽 카드 설치하기
- 홈페이지 들어가서 본인에게 맞는 그래픽카드를 찾는다
  - nvidia-390? 뭐이런걸 알려준다.
- 설치는 터미널에서..?

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
$ sudo apt-get install nvidia-375
```

- 설치가 끝나면 재부팅 해주기
  - 잘 되었는지 확인하는건 ```nvidia-smi``` 로 충분할 듯 하다.

# 2. CUDA/cudnn 설치하기
- [쿠다툴킷 다운로드 홈페이지](https://developer.nvidia.com/cuda-downloads)
- [cudnn 다운로드 홈페이지](https://developer.nvidia.com/rdp/cudnn-download)

## 2.1 CUDA 설치
- cuda를 깐 경로로 접근한다 (아마도 다운로드?)

```
# 실행
sudo sh cuda_9.1.85_387.26_linux.run
```

- 무슨 글이 쫘아아악 뜨는데 ```Ctrl``` + ```c```로 넘긴다.

- 질문 대답하기

```
Do you accept the previously read EULA?
accept/decline/quit: accept

Install NVIDIA Accelerated Graphics Driver for Linux?
(y)es/(n)o/(q)uit: n

Install the CUDA 9.1 Toolkit?  
(y)es/(n)o/(q)uit: y

Enter Toolkit Location  
 [ default is /usr/local/cuda-9.1 ]:

Do you want to install a symbolic link at /usr/local/cuda?  
(y)es/(n)o/(q)uit: y

Install the CUDA 9.1 Samples?  
(y)es/(n)o/(q)uit: n

```

- 환경변수 설정
  - 안에 본인 버전에 맞는 경로를 해줘야한다
  - cuda-9.1 부분
  - 이걸하고나서 home으로 가서 ```sudo gedit .bashrc``` 하면 제일마지막에 내가 쳣던게 들어가있는 것을 확인할 수 있다.


```
$ echo -e "\n## CUDA and cuDNN paths"  >> ~/.bashrc
$ echo 'export PATH=/usr/local/cuda-9.1/bin:${PATH}' >> ~/.bashrc
$ echo 'export LD_LIBRARY_PATH=/usr/local/cuda-9.1/lib64:${LD_LIBRARY_PATH}' >> ~/.bashrc
```

- 환경변수 적용 및 설치여부 테스트

```
$ source ~/.bashrc
$ nvcc --version
```

## 2.2 cudnn 설치
- 깔고 압축 풀고 그 경로에서 아래와같이한다.
  - cuda한테 복사하는 작업임. 따라서 오른쪽 경로는 본인에 맞게. 아마 버전 정도만 바꿔주면 됨

```
  $ sudo cp cuda/lib64/* /usr/local/cuda-9.1/lib64/
  $ sudo cp cuda/include/* /usr/local/cuda-9.1/include/
  $ sudo chmod a+r /usr/local/cuda-9.1/lib64/libcudnn*
  $ sudo chmod a+r /usr/local/cuda-9.1/include/cudnn.h
```

# 3. 도커 engine 설치
- 하..힘들다. 이젠 바로 도커엔진으로가자
  - 참고사이트
    - 진짜넘나감사
    - [여기여기](https://docs.docker.com/cs-engine/1.12/#install-on-ubuntu-1404-lts-or-1604-lts)
      - 중간쯤? 에 있는 Install on Ubuntu 14.04 LTS or 16.04 LTS 이다

- 아직도 sudo apt-get update를 정확히 모르지만 한다. 그다음 설치를 위해 필요한 재료 install

```
$ sudo apt-get update

$ sudo apt-get install --no-install-recommends \
    apt-transport-https \
    curl \
    software-properties-common

```

- 그 다음작업은 도커의 public key를 다운로드하고 import 하는 것

```
$ curl -fsSL 'https://sks-keyservers.net/pks/lookup?op=get&search=0xee6d536cf7dc86e2d7d56f59a178ac6c6238f52e' | sudo apt-key add -
```

- 뭔지몰라..해야함

```
$ sudo add-apt-repository \
   "deb https://packages.docker.com/1.12/apt/repo/ \
   ubuntu-$(lsb_release -cs) \
   main"

 ```

 - 마지막으로 도커엔진 설치!!

```
$ sudo apt-get update

$ apt-cache madison docker-engine
```

# 4. nvidia-docker 설치
- 드디어 대망의.. nvidia-docker
- 처음에모르고 여기부터 해가지고 다꼬임

```
# nvidia-docker 다운로드
$ wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0-rc.3/nvidia-docker_1.0.0.rc.3-1_amd64.deb

# 설치
$ sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```

- nvidia-docker가 깔렷지만 다되는건 아님
  - 일단 docker의 구성을 생각해보자
  - (이해하기로) 도커는 image와 container라는 두가지 요소가 (아마도 이거두개만 쓸거기때문에) 중요하다.
  - image는 주형틀 같은거고, container는 image를 이용해서 내컴퓨터에 진짜 놓여질 작품이랄까?  

- image 다운받기.
  - image가 container랑 같이 받아졌던거같은데..
  - 가라니까..ㅋㅋ둘다깔고 container는 내맘에 들게바꾸면되지
  - 우선 docker는 sudo 권한이있어야해서 ```sudo su```로 sudo 권한 항상먹혀있다고 가정
  - 뒤쪽에 ```:latest-gpu``` 부분을 수정하면 다른 image 받을 수있음 [image? 목록 site](https://hub.docker.com/r/tensorflow/tensorflow/tags/)

```
nvidia-docker run -it -p 8888:8888 tensorflow/tensorflow:latest-gpu-py3
```

- 다운받아짐
  - image 목록 확인하기 : ```nvidia-docker image```
  - container 목록 확인하기 : ```nvidia-docker ps -a```
  - 삭제 : ```nvidia docker rm (container id) 그리고 rmi (image id)```

- container 만들기 (이거 중요함)
  - ```nvidia-docker run -it -d -p (OS포트):8888 --name (container_name) -v (/data:/data) (docker_image_id)```
  - 일단 ```container_name```은 이제부터 container를 실행할때마다 만날친구
  - ```(/data:/data)``` : 도커와 내컴퓨터가 통신할? 마운트된 폴더? 매개체? 왼쪽이 내컴퓨터 오른쪽이 도커로 기억함.
  - ```docker_image_id``` nvidia-docker images에 있는 container에 넣고싶은 image의 아이디를 넣어주면됨.

- 실행
  - 도커에서나오는건 안에서 ```exit```
  - 그래도 도커는 돌고있다.
    - 실행중지는 ```nvidia-docker stop container_id_or_name```
    - 그담에 키고 exec 해야함 그건 ```nvidia-docker start container_id_or_name```

- 도커실행은 아래처럼

```
nvidia-docker exec -it (container_id_or_name) /bin/bash
```  

- 텐서플로 container는 exec과 동시에 쥬피터 접속이 가능하다.
  - 근데 토큰..
  - 토큰은 ```jupyter notebook list```로 확인이 가능함
  - ```IP주소:8888``` 로 원격접속도 가능 > 역시 토큰 찾아서 해줘야함. SSH로들어오든 뭐든 알아서해보셈.
