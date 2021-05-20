# MobileNetV2: Inverted Residuals and Linear Bottlenecks
## Abstract
- SSDLite
    - framework
    - object detection에 좋은 성능 냄
- Mobile DeepLabv3
    - mobile semantic segmentation model
    - inverted residual structure
        - thin bottleneck layer에 사이에 shortcut 연결
    - intermediate expansion layer
        - 경량 depthwise convolution 사용
            - image의 비선형성 feature 추출
- input과 output의 domain을 분리

## Introduction
mobile과 embedded application에서 연산량은 적으면서 정확도는 비슷한 모델을 원함
- inverted residual module 적용


