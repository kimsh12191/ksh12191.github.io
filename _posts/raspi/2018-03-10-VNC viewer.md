---
layout: post
title: 라즈베리파이 원격접속하기
modified:
categories: Raspi
excerpt:
tags: [Raspi]
image:
  feature:
---

# raspberry pi 원격접속하기
- VNC
- SSH
<br>
<br>





- 이게다..왠지 라즈베리파이가 블루투스 키보드가 안되서그래...
- 그래도 분명. 라즈베리파이도 포맷하는 날이올테니..시무룩

# 1. VNC 서버 이용하기
- 우분투에 vnc 서버를 설치해서 화면으로 직접 원격접속
- 설치

```
sudo apt-get update

sudo apt-get install tightvncserver

```

- 설치가 완료되면 ```vncserver :1``` 를 terminal에 입력해서 서버를 열어준다.
- 접속하고싶은 피씨에 vnc viewer를 깔고 ```IP주소:1``` 로 접속하면 끝

# 2. SSH 이용하기
- 뭔가 가장 개발자스럽지
- 컴퓨터에 부하도덜갈거같고
- vnc 서버는 라즈베리파이에 서버를 열어줘야함..
  - 심지어 켜서 vncserver :1 라고 쳐줘야함
- 우선 option을 ssh 가 가능하도록 바꿔주자
  - ```sudo raspi-config``` 로 접속
    - 일반적으로 8. advanced option에 ssh가 있다는데 (난그게업음.. 너무구버전?혹은신버전?)
    - 대신 4. Interfacing Options에 들어가있음
      - SSH 활성화시켜줌
- 그럼 다됨.
  - 아닌데..비밀번호는 어디서설정했지.. 기억이안남.ㅠㅠ..
- 원격접속하기  
  - ```ssh (접속할 ID)@(IP주소)```로 접속 가능
  - 일반적으로 라즈베리파이 id는 pi인듯
