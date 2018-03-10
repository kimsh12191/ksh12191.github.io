---
layout: post
title: Coordinate change
modified:
categories: machinelearning
excerpt:
tags: [Machine Learning]
image:
  feature:
---

# Coordinates change


- 굉장히 별거 아닌거 같아보이지만 중요함.
  - time domain -> frequency domain도 비슷한 컨셉으로 이루어지는거 같고..
  - __특히__ PCA의 경우로 차원 축소할 때, eigen vector를 basis로 가지는 coordinates로 변환하고, eigen value가 높은 것과 짝을 이루는 eigen vector의 basis만 남김으로써 차원축소를 진행함.

# process



- 같은 vector $$\vec{r}$$ 이지만 이 vector를 표현하기 위한 basis는 다양할 수 있다.
- 다른 coordinate에서 같은 vector 를 표현하는 방법에 대해서 생각해보자.
  - 아래 그림처럼 같은  vector $$\vec{r}$$지만 basis 가 달라지면 다른 [좌표] 를 지니게 된다.

  - 우리는 현재 [$$\hat{e}_1 \hat{e}_2$$] coordinate에서 $$x$$를 이용하여 표현되고 있는데, [$$\hat{q}_1 \hat{q}_2$$] coordinate 로 같은 vector를 표현하고 싶다.
    - 좌표계를 넘어가고 싶다.
    - 어떻게 넘어가지?
      - q basis를 알고있고, e basis와 e basis에서의 vector $$\vec{r}$$을 표현하기 위한 {$${x_1, x_2}$$}를 알고 있다.
      - 하지만 q basis에서의 vector $$\vec{r}$$를 표현하기 위한 좌표는 모른다.
      -  vector $$\vec{r}$$를 I coordinate에서 Q coordinate로 넘기기 위해서는 basis를 바꿀수 있는 (좌표를 바꿔주는) 함수를 찾아야한다.

  <center>
     <img src="/images/coord/coord1.png", width=250>
  </center>

  <center>
      Figure 1  basis e
  </center>

  <center>
     <img src="/images/coord/coord2.png", width=250>
  </center>

  <center>
      Figure 2  basis q
  </center>

<br>


- basis를 이용하여 좌표계 (coordinate) 상의 한 점(여기선 벡터?)을 표현한다.
- vector $$\vec r$$ y를 알고있다고 생각하고 한 점을 표현해보자.
  -   vector $$\vec r$$은 basis의 선형결합으로 표현이 가능하다.
  - $$\vec r = x_1\hat{e}_1 + x_2\hat{e}_2= y_1\hat{q}_1 + y_2\hat{q}_2$$
  -    $$\begin{bmatrix}\hat{e}_1&\hat{e}_2\end{bmatrix}\begin{bmatrix}x_1\\x_2\end{bmatrix}=I\begin{bmatrix}x_1\\x_2\end{bmatrix}=\begin{bmatrix}\hat{q}_1&\hat{q}_2\end{bmatrix}\begin{bmatrix}y_1\\y_2\end{bmatrix} =Q\begin{bmatrix}y_1\\y_2\end{bmatrix}$$

- 위의 식에서 x로 y를 표현하기위한 I와 Q로 이루어진 식이 만들어진다. (I (혹은 e)는 $$\begin{bmatrix}1 & 0 \\ 0 & 1 \end{bmatrix}$$ 인 identity 행렬, 기본적인 직교좌표계?)
  - x와 y사이의 선형변환을 찾아보자.

    - $$ \overrightarrow r  = x_1\hat{e}_1 + x_2\hat{e}_2  = y_1\hat{q}_1 + y_2\hat{q}_2 $$
    - $$
     =\begin{bmatrix}\hat{e}_1&\hat{e}_2\end{bmatrix}\begin{bmatrix}x_1\\x_2\end{bmatrix}=\begin{bmatrix}\hat{q}_1&\hat{q}_2\end{bmatrix}\begin{bmatrix}y_1\\y_2\end{bmatrix} $$
    - $$\implies  \begin{bmatrix}x_1\\x_2\end{bmatrix} = Q\begin{bmatrix}y_1\\y_2\end{bmatrix} $$
    - $$\implies  \begin{bmatrix}y_1\\y_2\end{bmatrix} = Q^{-1}\begin{bmatrix}x_1\\x_2\end{bmatrix}= Q^{T}\begin{bmatrix}x_1\\x_2\end{bmatrix}
    $$


  - basis $$\{\hat q_1 \hat q_2 \}$$ 로의 Coordinate change는 아래와 같이 표현할 수 있다.
    - $$ \underbrace{\begin{bmatrix}x_1\\x_2\end{bmatrix}}_{\text{coordinate in } I} \quad \underrightarrow{Q^T} \quad \underbrace{\begin{bmatrix}y_1\\y_2\end{bmatrix}}_{\text{coordinate in } Q} $$
    - 목표 coordinate의 basis를 알면 그것을 현재좌표계의 coordinate에 내적함으로써 coordinate change가 가능해진다.
