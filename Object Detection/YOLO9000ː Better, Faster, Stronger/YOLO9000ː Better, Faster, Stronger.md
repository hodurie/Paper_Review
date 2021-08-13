# YOLO9000: Better, Faster, Stronger
## Introduction
- Better
    - YOLO v1 보다 개선된 사항
- Faster
    - Darknet-19를 활용한 속도 향상
- Stronger
    - 9000개의 물체 탐지

## Better
- YOLO는 localization error가 높은 편
- recall이 낮음
- 이를 개선하기 위해 다음 8가지 방법을 사용
    - Batch Normalization
        - 모든 layer에 batch norm 적용
        - 정규화 효과를 얻을 수 있음
        - overfitting 없이 dropout 제거 가능
    - High Resolution Classifier
        - ImageNet의 input size를 448x448 까지 올려 fine tune
    - Convolutional With Anchor Boxes
        - fc layer를 conv layer로 대체
        - Anchor box 적용
    - Dimension Clusters
        - IOU를 고려한 k-means cluster 사용
    - Direct location prediction
    - Fine-Grained Features
    - Multi-Scale Training
    - Further Experiments

## Faster

## Stronger

## Reference
- [[논문 리뷰] YOLO v2 (2017) 리뷰](https://deep-learning-study.tistory.com/433)