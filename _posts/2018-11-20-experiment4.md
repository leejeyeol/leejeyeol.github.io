---
layout: post
title: 2018-11-20
---
## **Preparing**

#### **Experimental Type**
- 기능 실험


#### **Experimental goals**
- Autoencoder가 꼭 generative autoencoder여야 하는가?
- cycle loss와 GAN이 있다면 그냥 autoencoder도 prior를 따르도록 학습할 것 같다.

#### **Dataset**
- MNIST


#### **Step**
1. AE + GAN, AE + recon learn, AE + cycle learn , AE+ recon learn + cycle learn으로 실험 후 latent space visualize

* * *
#### **Result**
- AE + recon learn + cycle learn일 경우 VAE의 KLD term같은 regularizer가 없어도 prior를 따르게 학습하는 것을 확인.
