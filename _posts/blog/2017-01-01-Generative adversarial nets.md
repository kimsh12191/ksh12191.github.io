---
layout: post
title: Generative Adversarial Nets (GANs)
modified:
categories: Study
excerpt:
tags: []
image:
  feature:
---

# Generative Adversarial Nets (GANs)

- generative model
  - 라벨이 없는 데이터속에 있는 구조를 이해할 수 있음
  - 이해한 구조를 바탕으로 원래 데이터와 흡사한 데이터를 "generate".

## 구조
- 두개의 상반되는 뉴럴 네트워크로 구성
  - 이 네트워크의 역할은 마치 위조지폐를 만드는 사람과 위조지폐를 감별하는 사람의 관계와 흡사함
- Discriminative Network
  - 위조 지폐를 감별하는 친구.
  - P(Y|X) 를 평가함.
  - 데이터가 있을 때 이 데이터가 어떤 클래스에 속할지 판단
- Generative Network
  - 위조지폐를 만들어내는 친구.
  - joint probability P(Y,X)를 평가
  - 여기에서 x, y samples을 취득할 수 있음을 의미

![png](/images/GANoverview.png)
GAN overview. Source: https://ishmaelbelghazi.github.io/ALI

- 위 그림이 두 네트워크가 어떻게 움직이는지 나타내줌.
  - Generative network는 열심히  generator sample을 만들어냄
  - Discriminative network는 generator sample과 data sample을 비교해서 실제 데이터인지, 제너레이트 된것인지 판별함
- 기대 결과
  - 실제데이터와 구분하기 힘든 진짜같은 데이터를 제너레이트 하는 generative model을 만들자.

## 구현
- GANs 은 뉴럴 네트워크에 generative model을 가르칠 수 있는 방법을 제시함

- 쉬운예제로 생각해보자
- x : sample data, N(-1, 1)
- z : noise distribution, uniform(0, 1)
- G : 우리가 학습시킬 Generative network
  - we want to map points $z_1$, $z_2$, ... to $x_1$, $x_2$,...
  - $x_i' = G(z_i)$
  - 즉 G는 z를 이용해서 fake data x'를 만들어냄

![png](/images/generatefakex.png)
make fake x' using z and G. Source: http://blog.evjang.com/2016/06/generative-adversarial-nets-in.html

- D : Discriminative Network
  - 데이터 x를 받아서 진짠지 가짠지 판단
  - D(x)는 가능한 높게!
  - D(G(z))=D(x')는 가능한 낮게

## Optimize
- loss function of Discriminative Network
$$ log(D(x)) + log(1-D(G(z)))$$

- loss function of Generative Network
$$ log(D(G(z))) $$


- 뒤에 더있는데..아직 내용도잘모르고..지금쓴것도 사실 재정리해야함
