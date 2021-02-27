# Going Deeper with Convolutions
본 논문은 2014 ILSVRC에서 우승한 GoogLeNet을 다룸 

## GoogLeNet 이전 모델
AlexNet 모델
- 2012 ILSVRC 우승
- 8개의 layer 사용
- parameter 수 62M

## 딥러닝의 추세
1. stacked conv layers + fc layers(1 or more)
2. layer의 수와 layer size 증가
3. Dropout을 통해 overfitting 방지

## GoogLeNet
GoogLeNet도 추세를 따름
- stacked layers + fc layers
- layer 수 22개, wide한 layer
    - AlexNet 보다 layer의 수가 많음
    - AlexNet 보다 parameter 수 12배 적음
- Dropout 사용
- NIN(Network In Network) 사용

### Network In Network
NIN은 기존 conv layer에 MLP 추가
- 기존 conv layer는 GLM
    - 각 자리의 픽셀과 weight의 곱/합 연산
- conv layer에 MLP 추가
    - 비선형적 관계 표현 증가
<img src='image/Network In Network.jpg'>

### GoogLeNet의 단점
성능을 위해 depth와 width 늘림

1. depth 증가
    - parameter 수 증가
    - overfitting 위험
    - bottleneck
2. network size 증가
    - 연산 자원의 사용 증가
    - 연산량 증가

### GoogLeNet 단점 해결책
fc layer을 sparsely connected로 변경
- conv layer에서도 sparsely로 변경

하지만 sparse 한 structure은 하드웨어 계산에서 비효율
- 전체적으론 Sparse
- 내부적으론 Dense

## Inception Architecture 
Inception 주된 idea는 최적의 local sparse 구조로 근사화 하고 dense 요소로 변환

세 가지 필터의 크기 사용
- `1x1`
    - 국소적인 부분의 patch 생성
- `3x3`
    - `1x1` 보다 큰 범위의 patch 생성
- `5x5`
    - `3x3` 보다 큰 범위의 patch 생성


### `1x1` 필터 효과
채널의 수 감소
- `1x1`은 입력 데이터의 국소적인 부분 patch를 생성
- patch들은 비슷한 형태를 띰
- 이들을 clustering 하여 채널 수를 줄임
- 차원 감소
    - bottleneck 감소
    
<img src='image/Model.png'>
<img src='image/GoogLeNet.png'>


## Reference
- [Network In Network](https://arxiv.org/pdf/1312.4400.pdf)
- [Inception(GoogLeNet) 리뷰](https://kangbk0120.github.io/articles/2018-01/inception-googlenet-review)
- [Google Inception Model.](https://norman3.github.io/papers/docs/google_inception.html)