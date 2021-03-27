# What Uncertainties Do We Need in Bayesian Deep Learning for Computer Vision?
## Abstract
Uncertainty 종류
- Aleatoric uncertainty
    - 데이터에 내제 돼 있는 noise
- Epistemic uncertainty
    - 모델에 존재하는 uncertainty
위의 Uncertainty는 따로 측정
- Bayesian deep learning framework를 이용해 같이 측정할 수 있게 만듦  

학습 저하를 설명할 수 있는 loss function도 만듦

## Introduction
딥러닝은 맹목적으로 정확하다는 믿음이 깔려있음  
하지만 그렇지 않음
- 2016년 trailer의 하얀 부분을 하늘로 착각해 사망자 발생
- 이미지 분류에서 두 명의 아프리카계 미국인을 고릴라로 판별

Uncertainty의 필요성
- Bayesian deep learning을 활용해 Uncertainty를 구할 수 있음

Uncertainty 종류
- Aleatoric uncertainty
    - 데이터에 내제 돼 있는 noise에 대한 uncertainty
    - 두 가지로 나뉨
        - homoscedastic uncertainty
        - heteroscedastic uncertainty
- Epistemic uncertainty
    - 모델에 속해있는 uncertainty

