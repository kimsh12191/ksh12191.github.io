---
layout: post
title: Object Detection - fastRCNN
modified:
categories: machinelearning
excerpt:
tags: [DL, Object detection]
image:
  feature:
---

- Object Detection - fast RCNN 정리

[01. RCNN 정리](https://ksh12191.github.io/machinelearning/Object_Detection-(RCNN)/).
[02. Fast RCNN 정리](https://ksh12191.github.io/machinelearning/Object_Detection-(fastRCNN)/).

# 1. 단점 극복
  - RCNN은 잘되지만 느리다.. (안습)
  - 진짜로 쓰러면 빨라져야지. 어떤 부분을 빠르게 할 수 있을까? 느리게 만드는 부분이 대체어디지?
    - RoI를 만드는데 시간이 너무오래걸린다 (ex) seletive search같은) - 얘는 여기서해결을 못함
    - 모든 proposal region에서 cnn 을 이용하여 feature를 extract하는게 시간이 많이 소요됨. - 얘는 여기서 해결함
      - 어차피 사진은 한장이니까 거기에 여러번 CNN을 적용해서 feature를 extract하는게아니라 사진 한장에 대해서 한번에 CNN을 적용해서 feature 추출!
  - __image cropping을 input image에서 하는게 아니라 feature map에서 진행을 한다.__
  - __그림설명있는게 좋을거같은데__

# 2. Fast RCNN

- 아래 그림은 Fast RCNN의 구조를 보여준다.
  1. 앞쪽에 [proposal region]을 찾아내는 방법은 똑같다.
      - RoI(region of interest) : 우리가 집중적으로 보아야할 부분 (사각형)을 가리키는 단어
  2. 원본 이미지에 convolution 을 통해서 [conv feature map]을 획득한다.
  3. 뒤쪽에 분류하는 부분도 back propagation이 가능하도록 네트워크 구조로 되어있다.
      - [RoI pooling] 은 [사각형]이 모두다 다르니까 pooling으로 같게 만들어 주는 부분이다.
      - (동일한 크기로 만들어주는 이작업은 RCNN에서도 이루어지고 있었음)
  4. [RoI] 받아서, 어떤 사물인지 분류만 하는게 아니라 [bbox regressor]로 사각형을 좀더 조정함. 잘 찾을수있게,

 ![png](/images/RCNN/02_fastrcnn_structure.png)
          Figure 1 [2] Fast RCNN의 구조를 잘 보여주는 그림

# Fast RCNN?
- 이미지에 대해서 한번만 CNN을 적용함으로써 여러번 적용하던 RCNN에 비해서 속도가 더 빨라짐.
  - RCNN은 SVM, CNN으로 나눠져있는 구조라 학습과정이 한번에 되는게 아니라 왔다갔다함 (설명은 생략)
  - 반면 Fast RCNN은 pipeline이 쭉 연결되어있음. (end to end?)
    - __연결되있따는게 뭐지? 설명있으면 좋을듯__
- __또 Fast RCNN의 중요한사실__
  - Faster 부터는 RoI를 찾는데 걸리는 시간을 최소화하는데 힘을 많이 썻음
  - Fast RCNN의 기본적인 구조, RoI를 받았을 때, CNN으로 class, bbox regression하는것은 계속 가지고감(Faster나 Mask에서도 역시 거의 똑같은 구조로 이용되고 있음.)

# CODE
- 코드를 이용해서 설명하는게 좋을거같긴 한데, 필요한가? 사실 Fast RCNN은 그냥 CNN임. loss부분에 bbox regressor가 추가되어있는
- 아래 같은 느낌으로 이해하면 좋을듯. (build_fastRCNN 안에 함수를 여기서 설명하고있을 필요는 없을듯)
  - 조금 다르긴함, RoI를 받아서 feature map에서 그부분을 짤라낸다음 FC를 취해줌.
```python

_, C2, C3, C4, C5 = resnet_graph(input_image, "resnet101", stage5=True)
feature_maps = [C2, C3, C4, C5]
rcnn_class, rcnn_bbox = build_fastRCNN(rois, feature_maps)
```
- Loss
  - 그렇게 어렵지 않음
  - $L_{cls}$ : classification을 위한 Loss 부분 이게 낮아지면 분류성능이 좋아지겠지
  - $L_{loc}$ : regressor 부분, bbox를 좀더 정교하게 만들기 위한. 보통 L1 으로 predict 와 ground truth 사이의 거리를 계산하는 식으로 이루어짐
  - $\lambda$ : $L_{cls}$와 $L_{loc}$사이의 균형을 맞춰주는 역할.

---
- 감사합니다. 참고했어요

  [1] https://blog.lunit.io/2017/06/01/r-cnns-tutorial/

  [2] Girshick, Ross. "Fast r-cnn.
