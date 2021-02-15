# Interpretable Machine Learning – A Brief History, State-of-the-Art and Challenges
이 논문은 XAI에 대한 개관논문으로, 연구의 동향, 해석 기법들에 대해 설명하고 해결해야할 과제들에 대해 간략히 소개하고 있다.  

##  A Brief History of IML
**이전의 통계 모델**
- 특정 분포를 따른 다는 가정
- 모델의 복잡성을 사전에 제한

**ML**
- 비모수적, 비선형적 모델 가정
- 해석가능성보단 예측 성능에 초점을 둠

**DL**
- 딥러닝이 이미지 대회를 휩씁
- 해석가능한 모델(IML, XAI)이 대두
- 

**Today**
- IML에 대한 연구가 진행중
- 다양한 오픈 소프 소프트웨어를 통해 이용 가능

## IML Methods
IML 모델을 다음과 같은 기준으로 나눈다.
- analyze model components 
- model sensitivity
- surrogate models

### Analyze Model Components
#### Analyzing Components of Interpretable Models
모델 성분 분석은 모델의 구조와 연결 돼 있어 모델에 따라 다르다.  
또한 이 모델은 해석을 할 수 있는 구조와 매개 변수들을 갖는다.  
대표적으로 선형 회귀분석, 의사결정 나무, 의사결정 규칙이 있다.  

**선형 회귀분석**
- 변수에 대한 효과를 가중치로서 해석

**의사결정 나무, 의사결정 규칙**
- 규칙기반 ML
- if ~ then ~ 의 형식

위의 모델은 변수의 수가 증가하게 되면 해석이 불가능해진다.
이를 해결하는 방법으로 LASSO 모델을 통해 가지치기를 진행한다.
> LASSO란, 선형 모델에서 예측에 영향을 주지 못하는 coefficient의 값을 0으로 만드는 기법

#### Analyzing Components of More Complex Models
모델 성분 분석을 블랙박스 모델에도 적용해 부분적 해석을 가능하게 했다.  

**CNN**
- 합성곱 신경망
- 신경망의 특징맵을 시각화

**랜덤 포레스트**
- minial depth distribution
- Gini importance

일부는 monotonicity constraint 또는 수정된 손실 함수를 사용해 모델을 해석하기 쉽게 만들기도 한다.

하지만, 위의 해석은 특정 모델에서만 가능하기 때문에 다른 모델과 결합하여 사용할 순 없다.

### Model Sensitivity
#### Explaining Individual Predictions
ML의 Sensitivity 연구는 주로 다음과 같은 방법을 사용한다.
- model-agnostic
- 입력 데이터 조작
- 각 모델 예측 분석

이를 두가지 방식으로 나타낸다. 
- Local
- Global

**Local methos**
- 모델의 개별 예측을 설명
- Shapley values
  > 플레이어들에게 공정하게 금액을 나눌수 있는지(collaborative game)에 대해 해답을 줄 수 있음
- counterfactual explanations
  > what-if 시나리오를 이용하여 설명

또한 다른 모델은 Sailency maps 을 사용한다.
Sailency maps은 주로 CNN 에서 사용하며, input feature에 따라 output이 어떻게 변화하는지를 픽셀들의 heatmap을 통해 나타낸다.

#### Explaining Global Model Behavior
Global 분석 방법은 두 가지 방법을 사용한다.
- feature importance
- feature effect

**Feature Importance**
- 예측에 영향을 주는 순서대로 순위를 매기는 방법
- Permutation feature importance
- 일부 중요도는 feature을 넣었다 빼서 얼마나 달라지는 지를 측정

**Feature Effect**
- feature가 변화했을 때 output이 얼마나 변화하는 지를 측정
- Partial Dependence Plots
- Individual Conditional Expectation Curves
- Accumulated Local Effect Plots
- the Functional ANOVA
- 통계 기법을 활용

### Surrogate Models 
Surrogate Models은 다른 모델을 copy하여 나타낸다.  
또한 ML 모델을 black-box 모델로 취급하고 오직 필요로 하는 건 ML 모델의 input 데이터와 output 결과 뿐이다.

**LIME**
- Local Surrogate method

## Challenges
### Statistical Uncertainty and Inference
많은 IML 기법들은 설명력의 불확실정도를 수치화하지 않는다.
- 불확실성에 대한 수치화 필요

의미있는 속성을 추론하기 위해서 필요한 것들
- 구조적 가정
- 분포적 가정

### Causal Interpretation
ML모델이 어떤 때에 인과적으로 해석가능한지에 대해 연구가 진행되야 한다.

### Feature Dependence
서로 관련이 있는 변수들은 공통된 정보를 갖고 있어 특정 모델(랜덤 포레스트)에선 중요 변수로 뽑히게 된다.
- 모델이 잘못된 예측을 할 수 있음

### Definition of Interpretability
"interpretability"에 대한 용어들이 정립되지 않았다.

### More Challenges Ahead
통계 및 수학, 컴퓨터 과학의 분야에만 초점을 두는 것이 아닌 다른 분야들의 지식을 통해 모델을 어떻게 해석하고 설명할 것인지에 대한 고민도 이루어져야한다.