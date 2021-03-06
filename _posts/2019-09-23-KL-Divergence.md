---
title: "KL Divergence 정리"
date: 2019-09-23 08:26:28 -0400
categories: study
---

[팡요랩](https://www.youtube.com/watch?v=Dc0PQlNQhGY)의 강의영상을 참고해서 정리해봤습니다.



## 1. Entropy

뻔한 정보 = 확률이 높은 정보 : 흥미롭지 않다 = 정보량이 작다

따라서 확률이 낮은 흥미로운 정보는 정보량이 크다.

확률 $p(x)$ 와 정보량 $h(x)$ 는 **단조감소함수** 관계여야 한다.



이어서 독립적인 두 사건을 생각하자
- 독립적인 두 사건의 확률 = 곱
- 독립적인 두 사건의 정보량 = 합. 희석되지 않는다.



따라서 첫번째 조건과 결합하면 이러한 함수의 형태는 $-log$ 형태이다.



$$
h(x)=-log_{2}p(x)
$$



평균적인 정보량은 확률 * 정보량, 즉 기대값이다. 이 값을 **엔트로피**라고 한다. 



$$
H[X]=-\sum_x p(x)log_2p(x)=E_p[-log_2p(x)]
$$



Continuous한 경우는 다음과 같다.


$$
H[x] = \lim_{\Delta\to0}{\{\sum_ip(x_i)\Delta \ln p(x_i)\}}=-\int p(x)\ln p(x) dx
$$



Entropy를 **최대**로 하기 위해서는
- Discrete : Uniform distribution (확률이 모두 같은 경우)
- Continuous : Gaussian distribution (정규분포)

Entropy를 **최소**로 하기 위해서는

- 한 점에 확률이 다 몰려 있는 경우 0이 된다.





## 2. KL Divergence

실제 확률분포와 모델링한 확률분포에 차이가 생기면, 그에 따라 추가 비용이 발생하는데, 이를 이를 **Kullback–Leibler divergence (KL Divergence)**라고 한다. Discrete의 경우 다음과 같다.



$$
-(\sum_xp(x)log_2q(x))-(\sum_xp(x)log_2p(x)) = -\sum_xp(x)log_2\frac{q(x)}{p(x)}
$$



Continuous의 경우 다음과 같다.



$$
-\int p(x)\ln \frac{q(x)}{p(x)} dx
$$



KL Divergence는 아래와 같은 특징을 가지고 있다.

1. $KL(p\|q)\ne KL(q\|p)$

2. $KL(p\|q)\ge0$ ($p=q$ 일 때 0 만족)





## 3. Cross Entropy

Classification의 Loss 함수가 KL Divergence가 아닌 Cross Entropy인 이유는 다음과 같다.
- $p$를 근사하기 위해 $q$를 만든 것.
- $q$의 파라미터로 미분하면 $H(p)$가 사라진다.
- 따라서 $H(p,q)$를 Loss 함수로 쓰고, 사실상 KL Divergence를 쓰는 것과 같다.





## 4. Mutual Information

- 두 사건이 독립적이라고 하면 $p(x,y)=p(x)*p(y)$

- 두 사건이 독립적이지 않다면, KL Divergence를 이용하여 두 사건이 Independent와 얼마나 가까운지를 유추할 수 있다. 즉, 얼마나 정보량이 Mutual한 지 알 수 있다.

  
  $$
  I[x,y]=KL(p(x,y)||p(x)p(y))=-\int\int p(x,y)\ln(\frac{p(x)}{p(x,y)})dxdy
  $$

  

