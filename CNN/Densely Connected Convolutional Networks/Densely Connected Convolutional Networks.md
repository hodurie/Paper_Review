# Densely Connected Convolutional Networks
## Abstract
DenseNets의 장점
1. alleviate the vanishing-gradient problem
2. strengthen feature propagation
3. encourage feature reuse
4. substantially reduce the number of parameters

## Introduction
1. 이전 논문들 short path 사용 (이전 층의 값만 받는 식)
    -  우리는 모든 층을 연결시킴

2. ResNet은 features을 summation 함
    - 우리는 concatenating 함

3. 이전 논문은 $L$개 layer의 결합
    - 우리는 $\frac{L(L+1)}{2}$ 결합
    - 우리 모델은 dense connectivity pattern 때문에 `DenseNet`이라 부름

4. 불필요한 feature-maps을 재학습하지 않음
    - 기존 conv net보다 적은 파라미터 사용
    - ResNet은 identity transformation으로 정보 보존
        - BUT 많은 layer들이 거의 기여를 하지 않고 정보가 radomly drop 됨

5. DenseNet의 layer은 narrow 함
    - filter의 수가 많지 않음
    - collective knowledge를 추가
    - final classifier가 모든 feature-map을 반영하여 결정을 내림

6. 정보 및 gradient 전달이 개선 돼 학습하기 쉬움
    - 각 layer는 손실 함수와 input signal로 부터 gradient에 직접적으로 접근 가능
    
7. dense 연결이 정규화 효과를 가짐
    - overfitting 감소

## DenseNets
### Dense connectivity
ResNet : $x_{\ell} = H_{\ell}(x_{\ell-1}) + x_{\ell-1}$  
DenseNet : $x_{\ell} = H_{\ell}([x_0, x_1, \cdots, x_{\ell-1}])$

더하는 방식이 아닌 concatenate 하여 표현

### Composite function
$H_{\ell}(\cdot)$ : BN + ReLU + Conv

### Pooling layers
concat시 feature map의 크기가 다르면 연산이 불가능
- pooling을 이용해 feature map size를 줄임 
- 동일한 작업을 반복하는 layer을 하나의 block으로 만듦
- 여러개의 block들을 반복하는데 그 사이에 층을 transition layer라 함
    - conv와 pooling을 하는 layer

<img src='image/DenseNet.png'>

### Growth rate
DenseNet의 hyper-parameter : $k$
- $k$(growth rate) : $H_{\ell}(\cdot)$ 통과해 나오는 feature map의 개수

### Bottleneck layers
BN-ReLU-Conv(1x1)-BN-ReLU-Conv(3x3)-$H_{\ell}$
- Conv(1x1)을 통해 feature map의 크기를 $4k$로 맞춤

### Compression
모델을 간단하게 만들기 위해 사용
- transition layer에서 feature map의 수를 줄임
- $0 \leq \theta \leq 1 $, $\lfloor \theta m \rfloor$
    - $m$ : dense block의 feature map 수