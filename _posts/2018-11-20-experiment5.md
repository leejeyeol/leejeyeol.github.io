---
layout: post
title: 2018-11-22
---
## **Preparing**

#### **Experimental Type**
- 비교 실험

#### **Abstract**
베이스 논문과의 차이점을 '비슷한 역할을 수행하면서, 더 가벼운 모델임'으로 하려고 한다.

따라서 본 실험에서는 크게 두가지를 검증한다.

- 비슷한 기능을 할 수 있는 모델인가?
실제로 학습하였을 때 베이스 논문 and 우리 논문이 주장한 장단점이 발생하는가? 특히 mode collapse와 학습 안정성기능이 두 모델 모두 문제없이 동작하는지 확인해볼 필요가 있다.

- 우리의 모델이 더 가볍고 간단한 모델인가?
베이스 논문은 discriminator를 이용해 regularizer term을 추가하는데, discriminator로 신경망을 쓴다. 따라서 이것을 학습하는데 자원을 소비할 것이다. 또, autoencoding된 데이터를 사용하여 모델을 학습하는 부분이 추가되어있는데 단순히 mode collapse와 학습 안정성 개선을 위한 관점에서 볼 때 이런 추가적인 과정이 필요한지 불확실하다. 비슷한 기능을 유지하면서 더 가벼운 모델이던가, 가벼운 모델이면서 최대한 비슷한 기능을 유지한다면 차별점이 있을 것이다.


#### **Experimental goals**
- 두 개의 모델을 정확히 구현한다.
- 두 개의 모델에 대해 우리의 목적(mode collapse 방지, 학습 안정성 확보)을 정량화 할 수단을 마련한다.
- 두 개의 모델에 대해 모델의 복잡도(iteration당 걸리는 시간, 복잡도, 원하는 정량적 목표 달성을 위해 걸리는 시간)를 정량화 할 수단을 마련한다.
#### **Dataset**
- MNIST(빠른 검증)
- CelebA

#### **Step**
1. 정량화 수단 확보
	mode collapse : Wasserstein Critic
    학습 안정성 : strong discriminator
    모델 복잡도 
2. 
* * *
#### **Result**
