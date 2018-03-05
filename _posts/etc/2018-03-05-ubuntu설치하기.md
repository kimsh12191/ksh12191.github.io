---
layout: post
title: ubuntu 설치하기
modified:
categories: etc
excerpt:
tags: [ubuntu]
image:
  feature:
---

# Ubuntu 설치하기

# 1. 우분투설치를 위한 USB 만들기
- 흔히 말하는 부팅usb(?)를 우분투 용으로 만들어주어야 한다.
  - 나처음깔떈 14.04썻는데 이번엔 16.04한번가보자 (16.04가 한글은 지원잘해주는걸로 알고있음)
  - [우분투 iso 다운로드 링크](https://www.ubuntu.com/download) : iso 다운받고
  - [USB를 부팅 디스크로 만들기](https://rufus.akeo.ie/) : 이링크에서 rufus를 다운받자


- Usb에 iso를 넣자

<center>
   <img src="/images/ubuntu/01_install_ubuntu.png">
</center>

<center>
           rufus 키면 그림과같다.
</center>

- 부팅디스크로 만들 usb를 선택하고 (ISO보단 용량이커야함, 그리고 포맷됨) 빨간네모박스를 눌러서 ubuntu iso를 선택한다.

- USB가 만들어질거임

# 2. 우분투를 깔아보자
- 그전에 우분투깔 공간마련하기.
  - 일단 우분투가 들어갈 [파티션]이 따로있어야함. 가능하면 물리적인 하드자체가 다른게 좋을거같음
    - (실제로 본인은 그럤음. C드라이브는 윈도우, D드라이브의 반은 저장용, 나머지반은 우분투깔용)

    <center>
       <img src="/images/ubuntu/01_setting_partition.png">
    </center>

    <center>
      일로들어가면 파티션 수정이가능함(기존걸 축소하면된다.)
    </center>

- 이걸했으면 재부팅을 한다.
  - 까먹고 스샷안찍음
  - 바이오스 들어가서 부팅순서를 바꿈
    - 모르면다해봐도되는데, 윈도우는 일단 가장먼저가 아님. 무슨 usb가 제일먼저
    - 그럼 우분투 설치화면이 뜨거나.. 아니면 grub이 뜨거나(검은화면, 어쨌든 install ubuntu를 들어갈 것)

# 3. 우분투 설치 (세부)
- 자그럼이제 사진으로 퉁친다.
  - 그리고 약간의 설명?
<center>
   <img src="/images/ubuntu/01_ubuntu.png">
</center>
<center>
  1. 이것저것 쉬운 과정을 거치면.. 여기서 첫고민을 함// 그럼 둘다하면됨
</center>
<br>

<center>
   <img src="/images/ubuntu/02_ubuntu.png">
</center>
<center>
  2. 우분투를 어디설치할것인가? / 윈도우랑 같이 할수있을거같지?
</center>
<center>
  안됨/아무것도없는 파티션에할거에요 = 기타 선택
</center>
<br>

<center>
   <img src="/images/ubuntu/03_ubuntu.png">
</center>
<center>
  3. 도착하면. 지금컴퓨터는 드러운데 깔끔할수도 있음. 아까 2번인가?에서만든 텅빈 파티션이 보인다.
</center>
<center>
  이미지에서는 남은공간이라고 표현되어있음.
</center>
<center>
  저게클릭된건지 모르겠지만.. 여튼 클릭하고 '+' 를 누른다.
</center>
<br>


<center>
   <img src="/images/ubuntu/04_ubuntu.png">
</center>
<center>
  4. 일단 스왑영역을 만들자. 그림처럼하면되고. (아마 가상메모리?역할인듯 잘모르겠음)
</center>
<center>
  크기는 램의 배수로 넣으면된다고함
</center>
<br>

<center>
   <img src="/images/ubuntu/05_ubuntu.png">
</center>
<center>
  5. 본격. 우분투 들어갈 공간. (스왑영역만들고 또 남은공간 클릭하고 '+' 눌렀음)
</center>
<center>
  저거랑 똑같이하면됨 (크기는 다르게, 마운트위치는 'home' 이랑 비슷한거임 '/' 하는걸로)
</center>
<br>


<center>
   <img src="/images/ubuntu/07_ubuntu.png">
</center>

<center>
  6. 아까 남은공간이었떤 친구가  '/dev/sda5' 로 바꼇음.
</center>
<center>
  마지막으로 부트로더를 설치할 장치를 우분투가 깔릴 장치인 'sda' 와 똑같이 해준다.
</center>
<br>
