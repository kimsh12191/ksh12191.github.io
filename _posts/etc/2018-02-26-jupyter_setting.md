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

## 설정파일 생성

```
jupyter notebok --generate-config
```

- 설정파일 수정,
  - 설정파일은 `C:\Users\ [윈도우계정] \.jupyter` 디렉토리 안에 있다.
  - `jupyter_notebook_config.py` 수정
