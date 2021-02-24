# Very Deep Convolutional Networks for Large-Scale Image Recognition
본 논문은 2014년 ILSVRC에서 준우승한 모델인 **VggNet**을 다루고 있다.  
논문의 abstract에서 말하는 주된 기여도 다음과 같이 요약할 수 있다.  
```
1. 3 x 3 필터 사용
2. 16-19개의 weight layer 사용
```
기존의 CNN 모델의 경우 깊은 layer을 사용하지 않았다.  
반면 VGGNet은 layer의 개수를 늘리고 고정적으로 3 x 3 필터 사용해 모델의 정확도를 높였다.  


그럼 VGGNet이 무엇이며 어떻게 기여를 하였는지 자세히 알아보도록 하자.

## VggNet 구조
VggNet는 `224x224` 크기의 RGB 이미지를 입력으로 받는다.  
- 학습 데이터 셋에서 계산한 평균 RGB 값을 빼주는 전처리 작업 진행  

입력값을 `conv`층을 통과 시킴
- 필터의 크기는 `3x3`
- stride `1`pixel로 고정
- padding `1`pixel

`Maxpooling` 층을 통과 시킴
- `2x2`pixel window
- stride `2`

3개의 `Fully-Connected` layers
- 첫 번째와 두 번째 층은 `4096` channels
- 마지막 층은 `1000` channels


모든 `hidden` layers은 `ReLu`를 사용
- `Local Response Normalisation` 적용하지 않음

<img src='image/VggNet_Architecture.png'>

위의 표를 보면 `conv`층을 여러번 쌓아서 사용했는데  
이는 두 가지 측면에서 이점이 존재한다.
- 하나가 아닌 여러 개의 비선형 레이어를 사용해 결정 함수가 더 잘 구별하게 만듦
- 파라미터의 수를 줄일 수 있음

## 모델 학습
### 학습 파라미터
`multinomial logistic regression`를 최적화
- `momentum`이 있는 `mini-batch gradient descent` 적용
- batch size : `256`, momentum :`0.9`, $L_{2}$ : $5*10^{-4}$

첫 번째, 두 번째 FC 층에서 dropout : `0.5`  
learning rate : $10^{-2}$  
weight, bias 초기값
- 얕은 층(모델 A)의 weight를 사용
- 가중치 초기화 값 : $N(0, 10^{-2})$
- bias : `0`

학습 이미지를 `224x224`로 만들기 위해 랜덤하게 crop
- 이미지 crop 전에 이미지의 가로, 세로 중 작은 쪽을 `S`라 설정
- 비율에 맞춰 re-scale 하는데 `S`가 `224`이면 이미지 전체를 사용
- `S`가 `224`보다 클 경우 crop

## 모델 테스트
이미지의 크기를 다양하게 re-scale
- 이미지의 가로 및 세로 중 작은 쪽을 `224`로 맞출 필요 없음
