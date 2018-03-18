---
layout: post
title: Object Detection - RCNN
modified:
categories: machinelearning
excerpt:
tags: [Deep Learning, Object detection]
image:
  feature:
---

- Object Detection
  - [01. RCNN 정리](https://ksh12191.github.io/machinelearning/Object_Detection-(RCNN)/).
  - [02. Fast RCNN 정리](https://ksh12191.github.io/machinelearning/Object_Detection-(fastRCNN)/).

# 1. RCNN 모델의 간략한 구조
  <center>
     <img src="/images/RCNN/01_rcnn_structrue.png">
  </center>

  <center>
      Figure 1 [2] RCNN의 구조를 잘 보여주는 그림
  </center>

- 전체 구조를 보고, 알아가는게 중요할 것 같다.
  - RCNN 논문을 보면 첫장부터 이 그림이나온다. (그래서 이그림만 보고 논문을 다봤다 라고생각할 수도 있는것 같다. 하지만 object detection에서 딥러닝을 제대로 활용하는 시작논문에 가까워서, 한번 읽어보는 것도 좋은것 같다.)
  - 구조상 1번 2번은 기존의 방법론이 이용된다.
    - 그림에서 물체가 있을 것만 같은 지역을 찾아주는 알고리즘을 돌린다. (ex) selective search)
    - 그리고 많은 숫자의 region proposal을 얻는다.
  - 2번과 3번 사이의 길목에서 특이한 개념이 나온다. (혹은 당연하지만 응?이게 이래도되나 싶은)
    - 이미지의 비율을 무시하고 사이즈를 똑같이 맞추는 warp를 시행한다.
    - CNN 구조가 fully connected 를 위해서는 똑같은 사이즈의 input 을 요구한다.
  - 다음으로 CNN에 이 warp된 region을 input으로 넣어 학습한다.
    - 최근에는 이걸로바로 분류를 하지만 여기에서는 feature를 추출하는 개념으로 활용한다.
    - 또한 그림에는 나오지않지만 non maximun suppression을 적용하여, 같은 사물을 나타내는 수많은 region proposals 중에서 제일 좋은걸 하나만 골라낸다.
  - 분류는 SVM으로!!
    - SVM을 무시하는 경향이 없지않아 있었는데, 다음 논문인 fast RCNN 보면 그냥 딥러닝처럼 하는거랑 SVM하는거랑 별차이가 없다는 것을 보여준다. 심지어 튜닝 잘하면 CNN feature 추출 + SVM 이 더 좋을 수도 있음
      - 하지만 이런 pipeline 방법은 치명적인 함정이 있지.
      - 일단은 "용량" 이슈
      - 자세한건 fast RCNN 에서
  - 그림은 마치여기서 끝같지만 bbox regression이 있음
    - 이미 분류된 box들 중에서 제일 확률 높은 박스를 골라서 마지막으로 박스를 약간 수정하는 과정

- 따라서 전체프로세스는 다음과 같다.
  - 1. region proposal 추출
  - 2. pretrain 된 cnn에 region proposal을 input으로 넣어 domain specific 해지게 fine tuning
  - 3. fine tuning된 cnn을 이용하여 각각의 region proposal에 대한 feature를 취득한다. 그리고 이를 이용하여 SVM으로 클래스 분류
  - 4. 마지막으로 bbox regression 시행, 마지막 튜닝


# 2. RCNN, 그리고 Girshick의 논문에서 얻은 insight.

- 알려진것에 더하여, RCNN논문을 보면서 얻은 insight 들이 있따.
  - 이게 좋다, 혹은 아 이부분은 미래에 고쳐지겠구나. (우리는 대략적인 미래를 아니까)
- 총 네가지가 있따.

<br>

1. Region proposal
- 여기까지 딥러닝으로 하기에는 쉽게생각했을때는 떠오르지가 않음.
- 기존의 방법론과 잘 결합한듯?

2. Warped region
- 개선의 여지가 있는 부분
- appendix 까지 만들어서 설명을 해주는데 꼭, 비유를 망가뜨리면서까지 resize 해야하는건지..?
  - resize 자체가 필요한건 알겠지만.

3. Pretraining + fine turing
- 지금은 당연하게 쓰는 방법이지만 확실히 중요함
  - pretraining : 일반화된 feature들을 가져오는 것, 엄청 많은 수의 이미지를 학습시켜 놓으면 확실히 이미지에서 중요한 부분을 뽑는 일반화된 feature 를 만날 수 있을것
    - 많은 수의 이미지를 학습한 결과 생기는 아주 general한 conv feature는 이미지의 중요한 정보를 아주 잘 지니고있다고 할수있음.
    - fine tuning : domain에 맞게 feature를 추가 튜닝.

  - pretraining과 fine tuning에 있어서 Fc와 conv의 차이
    - 이 논문에 이걸 비교해놓은 부분이 있는데 흥미로움
    - conv 부분만 finetuning했을땐 성능향상이 미흡함 반면 fc를 추가하여 finetuning했을땐 성능이 확실히 향상됨
    - 일반화된 feature 정보는 conv가 많이 가지고있다. (새로운 이미지가들어온다고 해서 그 중요한 generalize된 faeture의 변화가 적은듯) 대신 fc가 domain에 맞게 많이 변해주는듯.

4. 상세 분류과정
- Bbox regression 몰랐는데. 정말
그림에도없음
  - Bbox regression : 사실 이거 만해도 성능 엄청오름
  - region proposal 에서 넘어온 box에서 시작해서, 변화시킬 차이만큼을 optimize 시킴
  - 이 자세한 object function 은 생략한다. 앞으로 계속 나온다
- Region proposal 모두에 대해서? 아니
  - 사물이랑 너무 멀리있으면, optimize 잘 안됨
  - 사물과 가장 가까운 박스
가까운?
    - Ground truth G 와 IoU가 가장 높은 박스만 이용해서 weight 찾으면 땡임

- Non maximum suppression
  - 같은 사물에 대해서 많은 roi 가 나올거.
    - IoU 가 일정이상인애들 중에서 제일 높은 score 를 가진 친구만 살림

# 결론?

- 이논문에서 흔히 아는 RCNN 구조만 얻을 줄 알았는데 생각보다 다른 많은 것을 얻을 수 있는듯?
  - pretraining 이나
  - bbox regression, 이게 여기서부터 나올줄이야
  - nms(non maximun suppression) , 이것도, region proposal 중에서 좋은거 잘 골라내는 것도 아주중요한 이슈라고 할 수있음.
- 또한, 나중에 많은 개선이 이루어질것으로 보이는 부분도 눈에 띄는거 같음.
  - region proposal resize하는 부분, 어떻게 변화하나 지켜보면서 논문을 보는것도 좋을듯.
  - 분류, bbox regression부분이 어떻게 이용되는지 보는것도 좋을것으로 보임
  - nms 부분도, 뭔가참신한게 나올까?
---
  [1] Girshick Ross, et al. "Rich feature hierarchies for accurate object detection and semantic segmentation.
