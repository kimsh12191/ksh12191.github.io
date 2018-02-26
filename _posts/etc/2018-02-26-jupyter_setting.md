---
layout: post
title: Jupyter 외부접속 설정
modified:
categories: etc
excerpt:
tags: []
image:
  feature:
---

# Jupyter 외부접속 설정(중요함)

- 맥 (사양이구리다) 으로 딥러닝을 하기위한 몸부림
  - 집 컴퓨터에 jupyter를 켜서 원격으로 접속하게 한다.
- 이게.. 아마도 윈도우기준?
  - 우분투에서 할때도 비슷했던거 같은데.

## 설정파일 생성

```
jupyter notebok --generate-config
```

- 설정파일 수정,
  - 설정파일은 `C:\Users\ [윈도우계정] \.jupyter` 디렉토리 안에 있다.
  - `jupyter_notebook_config.py` 수정


## 외부접속 허용
- `jupyter_notebook_config.py`에서 아래에 해당하는 부분만 수정하면 될듯

```
c.NotebookApp.allow_origin = '*'
```
```
c.NotebookApp.notebook_dir = '경로입력하기'
```

## 접속 암호 설정
- 암호설정
- 파이썬을 실행한다.

```python
from notebook.auth import passwd
passwd()
```

- 비밀번호생성하면 아래처럼됨
  - 아마도 아무것도 안쳐지겟지만 써지고있는거임

```python
>>> from notebook.auth import passwd
>>> passwd()
Enter password:
Verify password:
'sha1:e412d609ce63:59a4c8d32808a4e7284ebadcbba239479c8cd89e'
>>>
```

- 다시 `config` 돌아가서 password에 'sha1:e412d609ce63:59a4c8d32808a4e7284ebadcbba239479c8cd89e' 를 넣어줌

```
c.NotebookApp.password =
```

## 접속 포트 설정
  - 내가뭘 잘못했나? 딱히 여기적은포트로 안되는데...
  - 기본은 8888임 하나더키면 8889됨

```
c.NotebookApp.port =
```

## jupyter 실행
- 그냥 `jupyter notebook` 하면 localhost 켜짐. 원격접속 안됨

```
jupyter notebook --ip=[ip주소]
```
- 맨날까먹어서.. ip주소는 ipconfig를 통해 알 수 있음
  - IPv4주소가 ip주소임

---
- 그리고 지금은 안뜨는데 token? 뭐그런거 달라고 영어쫘라라락 뜨면서 뜨기도함. 그때는 커맨드창보면 jupyter 실행하면서 영어쫘라라락 써진 토큰 던져놨음 그거 복붙하면됨
