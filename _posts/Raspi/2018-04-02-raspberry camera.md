---
layout: post
title: 라즈베리파이 로 영상처리하기
modified:
categories: raspi
excerpt:
tags: [Raspi]
image:
  feature:
---

# raspberry pi 영상처리하기
- 왜?
- 카메라 연결
- opencv를 통한 영상취득



# 2. 라즈베리파이 카메라 연결
- 이건뭐. 별로 어렵지 않음.
- ```sudo raspi-config``` 여기로 들어가서 카메라 ```enable```만들어줘야 일단 라즈베리파이 카메라 연결이 됨.

## 2.1. 사진 찍어보기.
- OpenCV를 쓰지않고, 일단 카메라가 동작하는지 보기 위해서 사진을 찍어보자
  - 터미널에서 이명령어를 치면, 카메라가 잘 붙었다면, 사진이 찍힐 것이다. (라즈베리파이 카메라 쓸데없이 화질이 너무좋음, 그에반해 fps는 되게 후짐)

```
raspistill -o pic.jpg
```


- 이번엔 OpenCV로 영상을 찍어보자
  - 일단 'usb카메라'처럼 장치 인식을 시켜줘야한다. 그래야 OpenCV로 접근 가능 ```ls /dev/vidio*``` 쳐보면 카메라음슴.

```
sudo modprobe bcm2835 -v412
```

- 일단 이러면, 장치가 인식이 됨. ```ls /dev/vidio*``` 이젠 카메라 있음
  - 아마도, 이 작업은 부팅때마다 해줘야하는거 같음. ```etc/modules``` 파일에 드라이버 이름 등록해놓자. 마지막줄에 ```bcm2835-v412```를 넣어준다.
- 이제 OpenCV로 코딩을 시작해보자.

```python
import cv2
cap = cv2.VideoCapture(0)

while cap.isOpened():
  ret, img = cap.read()
  if ret:
    cv2.imshow('camera-0', img)
    if cv2.waitkey(1) & 0xFF == 27: # esc
      break
```
