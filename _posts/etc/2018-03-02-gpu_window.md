---
layout: post
title: window에서 tensorflow-GPU설치하기
modified:
categories: etc
excerpt:
tags: [python]
image:
  feature:
---

# window에서 tensorflow-gpu 하기

# 1. CUDA GPU설치하기
- CUDA toolkit 다운로드
  - [링크](https://developer.nvidia.com/cuda-downloads) : https://developer.nvidia.com/cuda-downloads
    -  근데 회원가입해야 받을 수 있음.. 하 귀찮
    - CUDA Toolkit 9.0 을 설치하자 (너무 최신을 깔아버리면 텐서플로가 지원안할 수도있음. - 9.1 깔았따가 다지우고 다시깔은자의...) 용량큼 1기가넘어감
    <center>
       <img src="/images/GPU/01_gpu_setting.png">
    </center>

# 2. cuDNN downloads
-  [링크](https://developer.nvidia.com/accelerated-computing-toolkit) : https://developer.nvidia.com/accelerated-computing-toolkit
  - Downloads 들어가서 잘 찾으면 Deep Neural Network(cuDNN) 이있따.
  - 설문을 하고나면 다운로드 받을 수 있음.
  - 본인이 설치한 CUDA Toolkit에 맞춰서 cuDNN 다운로드받기

- 우리는 CUDA를 깔면서 별생각없이 추천하는 대로 깔았을 뿐이지만 이런 경로가 생겼음. 아래 경로에 다운바은 cudnn압축을 풀어주자
  - 아래와 같이 파일이 구성되어있따.

  <center>
     <img src="/images/GPU/07_cudnn.png">
  </center>

  - 아래 경로에 붙여넣어준다.

  ```
  C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\
  ```

- 그리고 조심스레 텐서플로를 깔아준다.  ```pip install tensorflow-gpu``` 라고 친다 (tensorflow뒤에 gpu안붙이면 cpu버전깔림 조심.)
<center>
   <img src="/images/GPU/02_install_tf.png">
</center>
  - ```pip list```를 쳐보면 tensorflow-gpu 깔린걸 확인할 수 있따.

------
- 와.. cuda9.1 깔아서그랬던거같음.
- 뭔데 에러뜸(당황)
<center>
   <img src="/images/GPU/03_error_tf.png">
</center>

- ~~해결실패..~~
  - ~~찾아보니 환경변수를 설정안하면 모듈을 못찾는 에러가 난다고 한다.~~
  - ~~근데 환경변수가 어디있는지 모르니.. 아래 그림과같이 [내PC] 오른쪽클릭하고 속성으로 들어간다.~~

<center>
   <img src="/images/GPU/04_env_path01.png">
</center>

  - ~~그럼 아래와같은 창이 뜨는데 거기서 고급시스템 설정을 들어간다. 그럼 보임!! [환경변수]가~~

  <center>
     <img src="/images/GPU/05_env_path02.png">
  </center>

  - ~~당연히 들어간다. 이제 환경변수를 편집해보자.~~
    - ~~[환경변수]어딧는지도 모르는데 뭘 바꿔야할지 당연히 모름~~
    - ~~아래 그림처럼 path에 가서 [편집]을 누르면 저런창이뜸~~
    <center>
       <img src="/images/GPU/06_env_path03.png">
    </center>
    - ~~여기에다가 경로를 추가해준다.~~

    ```
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.1\bin
    ```

  - ~~근데 안고쳐짐? 와띠..~~
