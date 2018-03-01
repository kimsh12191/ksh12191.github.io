---
layout: post
title: Object Detection - RCNN
modified:
categories: machinelearning
excerpt:
tags: [DL, Object detection]
image:
  feature:
---

- Object Detection - RCNN 정리

(나중에 여기다가 다른 Object detection 링크도 달아야지)

# 1. Introduction
  - object detection
    - 모델의 입장에서 생각해보자. 모델이 영상을 본다.
      - step1. 그 영상속에서 어떤 물체가 있는지 없는지 찾는다.
      - step2. 만약 물체가 있다면 그 물체가 무엇을 나타내는지 분류한다.

# 2. Region Proposals
  - step1 부터 시작해보자. 영상(혹은 그림) 속에서 우리가 바라는 물체를 찾아야 한다.
    - 어떻게 찾게하지?
    - 가장 쉬운 방법은 다양한 크기의 window를 만든 후 그것을 slide 하면된다.
        1. window안에 물체가 있니? 있다/없다
        2. 옆으로 한칸 이동
        3. 다시 질문. 물체가 있니 없니?

  - Region proposal algorithm
    - sliding window는 무식함. 당연히 느림
    - 좀더 빠르게 물체가 있을법 한곳을 찾아내는 다양한 알고리즘들을 말함. ex) selective search?

# 3. R-CNN
  - R-CNN은  넘나 유명해서 사실 논문을 읽어보지는 않았다. (하지만 딥러닝 object detection의 시작!?!) 그림만 봐도 알거같은 기분같은 기분
  - 간략하게 설명하면 R CNN은
    1. region proposals algorithm으로 사물이 있을것 같은 영역을 찾고
    2. CNN으로 그 영역의 중요한 feature 를 추출한 후
    3. SVM으로 그 영역의 사물이 어떤 것을 나타내는지  classify한다. (와 뭔가 난잡한데? 빡세다.)


 ![png](/images/RCNN/01_rcnn_structrue.png)
          Figure 1 [2] RCNN의 구조를 잘 보여주는 그림

 - 이 그림만 어느정도 이해했으면 RCNN에서 건질거 다건진듯

 - __좀더 상세 STEP설명__
    - 어디감?

 - 이 친구는 잘됨/하지만 속도가 느리지. 가장 강력한 속도가 느린 이유는 이미지 1장당 region proposal개수 만큼 CNN 연산을 해줘야해서  inference 속도가 매우 느림.

---
- 감사합니다. 참고했어요

  [1] https://blog.lunit.io/2017/06/01/r-cnns-tutorial/

  [2] Girshick, Ross, et al. "Rich feature hierarchies for accurate object detection and semantic segmentation.
