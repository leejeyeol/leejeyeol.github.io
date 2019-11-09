---
layout: post
title: Preprocessing
categories : [ML,DL]
use_math: true
---
Preprocessing
================

Mean Normalization
----------------   
각 데이터 벡터에 그 벡터의 평균을 빼서 0근처로 이동시키는 방법

Standardization 
---------------
mean normalization에 더해서 그 벡터의 표준편차를 나누어 그 벡터의 각 feature에 대한 스케일까지 맞추는 방법.
ex) scatter plot을 그렸을 때 feature 1과 feature 2의 스케일이 다를 경우 한쪽으로 치우친 plot이 나오는데 standardization을 하면 치우치지 않은 plot을 볼 수 있음
standardization된 데이터들의 covariance matrix는 대각성분(각 데이터의 variance)이 1이기 때문에 사실상 correlation matrix이다.

Whitening
----------------
Whitening transformation 이란 covariance matrix가 알려진 random variable의 vector를 covariance matrix가 identity matrix인 새로운 variable로 변경시키는 linear transformation이다. 
이것은 곧 데이터들이 uncorrelated되고 variance가 1이 된다는 것을 의미한다.
이것이 whitening transformation이라 불리는 이유는 input vector를 white noise vector로 바꿔주기 때문이다.
하는 방법은 mean nomalization을 해서 평균을 0으로 맞춘 후(이 작업을 먼저 하면 covariance matrix를 계산하기 쉬워진다. $XX^{T} / n$),
decorrlation이라는 작업을 수행해서 correlation을 제거하여 0으로 맞춘다.
이후 standardization을 할때처럼 feature들의 스케일을 맞추고 대각성분을 1로 만들면 covariance matrix가 identity matrix가 된다.

이 작업에서 decorrlation은 어떻게 하는걸까?
데이터의 scatter plot을 그리면 correlation이 있는 경우 기울기로 표현되는데, 데이터 벡터들을 잘 rotation시켜서 기울기를 없애준다면 correlation이 없어진다고 할 수 있다. 
이를 어떻게 수행할 수 있을까? covariance matrix의 eigenvectors를 이용한다. 
원리는 covariance matrix는 기하학적으로 decorrelated data와 rotation,scaling operator로 decomposition될 수 있는데, 
여기서 rotation matrix가 covariance matrix의 eigenvector들을 coloumn으로 하는 matrix이다.(https://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/)
이를 이용하여 rotation시키면 eigenvector들을 basis로 하도록 데이터들이 회전한다. 
(scaling matrix는 eigen value를 대각성분으로 하는 대각행렬이 된다. 이는 decorrelate된 데이터의 분산이 곧 eigenvalue임을 의미한다. 
eigenvalue는 eigenvector들의 방향의 분산과 관련이 있는데 decorrelate된 데이터는 basis가 eigenvector이기 때문에 decorrelated 데이터의 분산은 eigenvalue이다.)

결과적으로, mean subtraction을 수행 한 후
covariance matrix를 구하고
covarinace matrix를 이용해 eigenvector matrix를 구하고
mean subtraction된 데이터에 eigenvector matrix의 tranpose를 곱하고
이를 std로 나누면 해당 데이터는 covariance matirx가 identity matrix인 white noise가 되고
이를 whitening 했다고 한다.


대량의 데이터에 대한 preprocessing
---
지금까지는 소수의 데이터에 대하여 preprocessing을 했지만, 대량의 데이터를 학습시키기 위해 sgd기반의 mini batch learning을 하는
요즘 모델들은 약간 다른 방법의 preprocessing을 수행한다.

이미지 데이터의 경우, 한 이미지 데이터 안의 mean과 std를 사용해서 standardization을 하지 않고, 
모든 데이터에서 같은 index에 있는 값들의 평균값을 이용해 모든 데이터의 mean image를 만들고 이를 subtraction 한다.
이 방법이 인공신경망을 사용한 학습을 할 때 좋은 결과를 냈다고 한다.
이 방법을 사용할 때는 training data들의 mean image를 이용하며 이를 inference 단계에서도 사용한다.