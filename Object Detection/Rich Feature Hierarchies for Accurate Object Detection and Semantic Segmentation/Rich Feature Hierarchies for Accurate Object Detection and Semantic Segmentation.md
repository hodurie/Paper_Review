# Rich Feature Hierarchies for Accurate Object Detection and Semantic Segmentation
## Abstract
이전 모델보다 mAP를 30% 이상의 성능 향상
- 모델이 간단하면서 확장성이 높음

주된 insight
- localize와 segment object를 위해 bottom-up region에 ConvNet 적용
- domain-specific fine-tuning

## Introduction
R-CNN 알고리즘
<img src='image/R-CNN.jpeg'>

1. 이미지를 입력 받음
2. 2000개의 region proposals 추출
    - warping을 통해 정사각형의 이미지로 변환
3. CNN을 이용해 region proposals의 feature 계산
4. 선형 SVM을 이용해 class 분류

## Object detection with R-CNN
R-CNN은 세 가지의 모듈로 구성 됨
- category-independent region proposals 생성 모듈 
- region에서 고정된 feature vector를 추출하는 CNN 모듈
- 분류를 위한 SVM 모듈

### Module design
1. Region proposals
    - selective search 사용
    > 1. 이미지 초기 세그먼트를 정하여 수많은 region 생성
    > 2. greedy 알고리즘을 사용해 각 region을 기준으로 유사한 부분을 병합
    > 3. 병합된 하나의 큰 부분을 region proposal로 제안

2. Feature extraction
    -  CNN을 사용해 region proposal로 부터 4096차원의 vector 추출
        - 5 개의 Conv layer와 2 개의 fc layer로 구성
        - region proposal을 CNN의 input으로 넣기 위해 고정 된 크기로 줄임


## reference
- [R-CNN(Regions with CNN features) 논문 리뷰](https://jaehyeongan.github.io/2019/10/10/R-CNN/)