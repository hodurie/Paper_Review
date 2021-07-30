# You Only Look Once: Unified, Real-Time Object Detection
## Abstract
- object detection을 회귀 문제로 바꿔 풂
- 전체 이미지를 한 번의 평가로 bbox와 class 확률 추정
- 빠르고 다른 실시간 detector보다 정확도가 높음
- 최신 detection system보다 localization error가 높지만 false positive는 적음
- 객체에 대한 일반화된 표현을 학습

## Introduction
- 사람은 한 번 보고 이미지에서 물체가 어딨는지 확인 가능
- 현재의 detection system은 여러 과정을 거쳐 객체를 탐지
    - DPM의 경우 sliding window를 거쳐 객체 탐지
    - R-CNN의 경우 region proposal method를 통해 객체 탐지
    - 해당 모델들은 복잡한 pipeline을 사용 
        - 최적화 하기 힘들고 느림
- YOLO의 경우 객체 탐지를 단순 회귀문제로 변형해 한 번만 보고 탐지 가능
- YOLO 특징
    - 엄청 빠름
        - 단순 회귀문제로 바꿔 복잡한 pipeline이 필요 없음
    - 이미지 전체를 보고 추론함
        - sliding window와 region proposal과 달리 전체 이미지를 보고 학습 및 테스트 함
            - class에 대한 문맥 정보와 외형 정보를 학습
    - 객체에 대해 일반화된 표현 정보를 학습 함
        - 실사 이미지로 학습 하고 그림 이미지로 테스트하면 다른 모델보다 성능이 좋음 
        - 이미지에 대한 일반화 된 정보들을 학습하여 다른 영역의 이미지가 들어와도 준수한 성능을 냄
    - 빠른 속도로 물체 탐지로 최신의 기술들 보단 성능이 떨어짐
        - 특히 작은 물체를 탐지하기 힘듦

## Unified Detection
- object detection의 요소들을 single neural network로 통합
    - 전체 이미지의 feature를 이용해 모든 class에 대한 bbox를 구함
    - simple piepline으로 end-to-end 학습이 가능
    - 속도도 빠르면서 준수한 average precision 유지
  
- YOLO model

<img src='images/fig2.png'>

1. 이미지를 $S \times S$ grid로 나눔
2. 객체의 중심이 grid cell에 속해있으면 grid cell이 해당 객체를 탐지
3. 각 grid cell은 bbox와 confidence score를 예측