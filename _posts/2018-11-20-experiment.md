---
layout: post
title: 2018-11-20
published : false

---
## **Preparing**

#### **Experimental Type**
- 성능
- 비교 실험


#### **Experimental goals**
- pretrained classifer로 VAE-GAN의 능력 검증
- 각각 Vanila, Autoencoder, Variational Autoencoder, VAE-GAN으로 학습한 pretrained model을 사용하여 Classifier를 훈련시켜 그 차이를 보려 한다.

#### **Dataset**
- CIFAR-10
- CIFAR-100(optional)

#### **Step**
1. 32x32 네트워크 설계(done)
2. vanila를 제외한 3개의 네트워크 학습
3. pretrained model을 사용하여 4개의 classifier 학습(동일 epoch)
4. validation set에 대한 accuracy, ROC 커브 확보

* * *
#### **Result**
$${A}^{B}$$

