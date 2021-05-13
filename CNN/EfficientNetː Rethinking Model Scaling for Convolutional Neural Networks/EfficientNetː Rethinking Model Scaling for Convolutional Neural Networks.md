# EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks
## Abstract
- 새로운 스케일링 방법 소개
    - 간단하면서 고효율을 내는 scaling 제시
    - **compound coefficient**
- 새로운 neural architecture 소개
    - **EfficientNets**

## Introduction
기존 모델
- depth를 깊게해 모델 성능 향상
- width를 넓혀 모델 성능 향상
- resoluton을 올려 모델 성능 향상

이전 논문들을 통해 scale up의 중요성 파악
- width와 depth에 대한 상관 관계 제시

**width**, **depth**, **resolution**을 동일하게 scale up method 제시
- compound scaling method
- 임의의 값을 갖고 scaling 하는게 아닌 특정 상수의 값을 이용해 균일하게 scale

<img src='images/fig2.png'>

- (e) resoultion을 높이고 층을 깊게 만들며 width를 넓힘

## Compound Model Scaling
### Problem Formulation
ConvNet Layer $i$ 는 다음과 같이 정의 할 수 있음
- $Y_i = \mathcal{F}_i(X_i)$
    - $\mathcal(F)_i$는 연산자, $Y_i$는 output tensor, $X_i$는 input tensor
    - $X_i$의 크기는 $< H_i, W_i, C_i >$

다양한 stages로 나눠진 architecture 는 다음과 같이 정의 할 수 있음

<img src='images/compound_formulation.png' width="500">

- $\mathcal{F}^{L_i}_i$는 $\mathcal{F}$ stage $i$에서 $L_i$번 반복
- 위의 식도 모든 요소들을 고려하기 힘듦

<img src='images/efficientOpt.png' width='500'>

- 위와 같이 간소화
- network의 정확도를 최대화 할 수 있는 coefficient $d, w, r$을 찾는 쪽으로 식 정의
