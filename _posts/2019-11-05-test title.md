---
layout: post
title: test title
categories : [ML,DL]
use_math: true
---
<!--밑바닥부터 시작하는 딥러닝--->

밑바닥부터 시작하는 딥러닝
================
복습겸 놓친부분 정리

Chapter 1 생략  
----------------  
Chapter 2 퍼셉트론  
----------------  
**퍼셉트론** : 다수의 신호를 입력으로 받아 하나의 신호를 출력.  
가장 단순한 퍼셉트론은 2 신호를 입력으로 받아 각각 가중치를 곱하고, 더한 뒤 해당값이 특정한 값(임계값.$\theta$)를 넘어설 때 1을, 아니라면 0을 출력하는 퍼셉트론이다.

가중치(weight)는 각 신호의 중요도,혹은 영향력이라고 생각할 수 있다. 첫번째 신호에 대한 가중치가 높고 두번재 신호에 대한 가중치가 낮다면 결과는 첫번째 신호의 강도에 크게 영향을 받을 것이다.

가장 간단한 퍼셉트론의 식은 다음과 같다. (w는 가중치, x는 입력신호, y는 출력신호) 

$$ y =  \begin{cases} 0 & w_{1}x_{1}+w_{2}x_{2} \leq \theta\\1 & w_{1}x_{1}+w_{2}x_{2} \geq \theta\\ \end{cases} $$
 만들었기 때문에 별거없어보이지만, 이후 적합한 weight를 자동으로 찾아내는 방법들을 언급할것이다.

$w_{1}x_{1}+w_{2}x_{2}$ 에 bias $b$를 더하여 $w_{1}x_{1}+w_{2}x_{2}+b$의 형태로 사용할 수 있다.(bias는 따로 고려하기도 하지만 weight와 묶어서 같이 weight로 표현하기도 함)
$w_{1}x_{1}+w_{2}x_{2}+b$는 선형방정식 형태이다. 따라서 weight를 조절하는 것은 $x_{1}$과 $x_{2}$를 축으로 하는 vector space에서 직선의 기울기와 bias를 조절하는 것으로 생가갈 수있다. 
그렇기에 가장 단순한 퍼셉트론의 weight를 조절하는 것으로 AND, NAND, OR같은 선형 문제는 풀 수 있지만 XOR같은 비선형 문제를 풀 수 없다.


  

이 퍼셉트론의 $w_{1}$과 $w_{2}$를 잘 조절하면 이 퍼셉트론은 AND, OR, NAND 게이트를 구현할 수 있다.  
똑같은 구조를 가진 퍼셉트론이 weight만 바꾸면 다른 함수가 된다는 것은 중요한 포인트이다.  
지금은 weight를 직접 조절해서 우리가 원하는 함수가 되도록 만들었지만 나중에는 weight가 자동으로 조절되는 방법을 소개할것이다.



chapter 3 신경망

softmax 함수
overflow를 피하기 위해 상수를 이용해서 구현(밑바닥 93)
inference 단계에서는 계산하지 않고 max를 하는게 계산비용의 이득(지수함수 계산이 비쌈)

accuracy를 직접 objective function으로 사용하게 되면 weight에 대한 미분값이 대부분의 구간에서 0

gradient는 모든 변수의 편미분을 벡터로 정의한것.$(frac{\delta f}_{\delta x_{0}},\frac{\delta f}_{\delta x_{1}})$
gradient descent 는 각 변수에 해당 변수에 대한 편미분값 * learning rate를 빼는 것으로 이루어짐.
따라서 변수 벡터 - gradient*learning rate로 표현된다.(당연하지만 ascent는 빼는게 아니라 더한다.)
미니 배치 케이스의 경우 gradient를 각 배치에 대하여 평균내어 사용한다.

필요한 미분은 수치미분으로 이루어짐. 
순수한 수치미분으로도 해결할 수 있지만 이는 느린 편이고, 해석미분과 back propagation을 사용하면 고속화할 수 있다(DP처럼 동작함.)

chain rule 합성함수의 미분은 합성함수를 구성하는 각 함수의 미분의 곱으로 나타낼 수 있다.

책에서는 계산 그래프를 이용한 방법으로 backpropagation을 설명하는데... 어떻게 보면 수식이 더 이해하기 쉬운것같기도 하다.
pytorch에서 구현을 계산그래프로 하기 때문에 계산그래프도 더 완전히 이해하면 좋을 것 같다.

chapter 6 Techniques 
----------
**Optimizers** 
SGD
모멘텀(속도,관성의 개념 도입)
Adagrad(각각의 weight에 대한 각각의 learning rate를 적응적으로 조절한다. gradient에서 미분값이 큰 값일수록 learning rate가 줄어듬)
RMSProp(Adagrad는 기울기의 제곱을 계속 더해가며 이를 이용해 갱신함으로  점점 갱신강도가 약해져 나중에는 전혀 갱신되지 않는 문제가 있다.
RMSProp은 과거 기울기의 비중을 점점 줄이고 최근 정보의 비중을 늘리는 Exponential Moving average로 learning rate를 결정하여 갱신량을 유지함.)
ADAM (모멘텀 + Adagrad. 관성을 추가하고 여기에 적응형 learning rate를 적용한다.) 

**Weight Initialization**
각 레이어의 활성화값이 activation function의 기울기를 0으로 하는 값이 적을수록, 그리고 한 값으로 치우치지 않을수록 좋다.
그렇지 않으면 gradient vanishing 현상이 일어나거나 신경망의 학습이 더뎌진다.
Sigmoid나 Tanh를 activation function으로 쓸때는 Xavier 초기값을, ReLU를 쓸 때 He 초기값을 쓰면 좋다.

**Batch Normalization**
BN은 각 layer에서 activation function에 입력되기 전(이나 후), 데이터들이 평균 0 분산 1이 되도록 정규화한다.
그리고 정규화된 값에 scale 연산과 shift연산을 수행하며, 이 연산의 피연산자는 학습과정에서 weight와 함께 학습된다.
이 연산은 미분가능하여 backpropagation이 가능하다.
각 계층의 데이터값을 정규화하면 학습속도가 빨라지고 weight initialization의 영향을 덜 받으며, 오버피팅을 억제해준다.
