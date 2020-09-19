---
layout: post
title: Information Theory 정리
---
## Shannon Information Content

$h(X=x) = \log_{2}{(\frac{1}{p(X=x)})}$

def :  random variable X에서 x 가 가지는 정보량.

- p(x)가 클수록 정보량은 완만하게  감소한다.
- p(x)가 작아질 수록 정보량은 가파르게 증가한다.

---

## Shannon Entropy (Original)

$H(X) = \sum_{I} -p(x_{i}) \log_{2}{p(x_{i})}$

def : random variable X 가 가지는 평균 정보량.  

- random variable X을 optimal 하게 부호화 했을때 ,  X를 하나 표현하기 위해 비트길이의 기대값.

---

## Shannon Entropy  

- random variable X의 놀람의 정도(a Measure of Surprise) 또는 불확실성의 정도(a Measure of Uncertainty)

-  ### Discrete random variable

   $H(X) = \sum_{I} -p(x_{i}) \ln{p(x_{i})}$

   - $H(x) \ge 0$

- uniform 할때 최대가 된다.

- 유효한 x (p(x)가 0이 아닌 x) 의 개수가 커질수록 $H(X)$도 커진다. 

- ### Continuous random variable

  $H(X) = \int -p(x) \ln{p(x)} dx$

  - 평균이 $\mu$ , 분산이 $\sigma^{2}$인 연속확률분포의 경우 Normal Distribution일 때 최대가 된다.

---

## Joint Entropy

$H(X, Y) = \sum_{x \in X} \sum_{y \in Y} - p_{X,Y}(x,y) \ln {p_{X,Y}(x, y)}$

- $X,Y$가 독립이면 $H(X) + H(Y) = H(X, Y)$
- 일반적으로 $H(X, Y) \le H(X) + H(Y)$
- {X, Y} 의 놀람의 정도(Surprise) 또는 불확실성의 정도(Uncertainty)

---

## Conditional Entropy

- ### Conditional Information Content :

  - $h(x \vert y) = -\ln{p(x)}$

   -  $h(x, y) = h(x \vert y) + h(y)$

- ### Conditional Entropy

  - $H(X \vert Y=y) = \sum_{x \in X} - p_{X \vert Y}(x \vert Y=y) \ln p_{X \vert Y}(x \vert Y=y) $
  
  - $H(X \vert Y) = \sum_{y \in Y} p_{Y}(y) \sum_{x \in X} - p_{X \vert Y}(x \vert y) \ln {p_{X \vert Y}(x \vert y)}$
  
  - $H(X, Y) = H(X \vert Y) + H(Y)$
  
  - $ X,Y$가 독립일 경우, $ H(X \vert Y) = H(X) $ 
  
  - $ X,Y $가 종속일 경우, $ H(X \vert Y) < H(X)$
  
    

---

## Cross Entropy

$ CE(p_{X}(x) \vert \vert p_{Y}(y)) = \sum_{x \in X} - p_{X}(x) \ln{p_{Y}(Y=x)} $

- X를 Y의 distribution을 기준으로 정보량을 매겼을 때 얻어지는 평균 정보량. (Sampling은 X로 하되, Measure of Suprise는 Y을 기준으로 매겼을때)
- $p_{Y}(y)$가 $p_{X}(x)$ 에 가까워질 수록 Cross Entropy는 줄어든다.
- $p_{X}(x) = p_{Y}(y)$ 이면 Cross Entropy는 최솟값으로 $ H(X) $를 같는다. 
  - Gibbs inequality

---

## KL Divergence

$D_{KL}(p_{X}(x) \vert \vert p_{Y}(x)) = \sum_{x \in X} p_{X}(x) \ln \frac{p_{X}(x)}{p_{Y}(x)}$

- $D_{KL}(p_{X}(x) \vert \vert p_{Y}(x)) = H(p_{X}(x))  + CE(p_{X}(x) \vert \vert p_{Y}(x))$
- $ p_{X}(x) = p_{Y}(Y=x) $이면 0이된다.
  - Gibbs inequality
- X의 distribution 에서 Sampling 한 데이터를 기준으로 $p_{X}(x)$ 와 $p_{Y}(Y=x)$의 값이 다를수록 KL divergence 값이 커진다.

---

## Mutual Information

$I(X;Y) = D_{KL}(p_{X,Y}(x, y) \vert \vert p_{X}(x)p_{Y}(y))$

- $I(X;Y)= \sum_{y \in Y} \sum_{x \in X} p_{X,Y}(x,y) \ln { \frac{p(x, y)}{p(x)p(y)}}$

- $I(X;Y)= \sum_{y \in Y} p(y) \sum_{x \in X} p_{X \vert Y}(x \vert Y=y) \ln { \frac{p_{X \vert Y}(x \vert Y=y)}{p(x)}}$

  $= E_{Y}[D_{KL}(p_{X \vert Y}(X \vert Y) \vert \vert p_{X}(x))]$

- $I(X;Y) = I(Y;X)$

- $I(X;Y) = H(X) - H(X \vert Y)$

- $I(X;Y) = H(Y) - H(Y \vert X)$

- $I(X;Y) = H(X) + H(Y) - H(X, Y)$

- $I(X;X) = H(X)$ (self information)

- Information Gain 이라고도 불린다.

- KL divergence이므로 언제나 0 이상이다.

- X, Y가 독립일때 Mutual Information은 0이 된다.

- X가 가지는 불확실성에서 Y가 given 일때  X가 가지는 불확실성을 뺀 값

- Y를 알게되면서 덜어내게 된 X에 대한 불확실성

---

## Pointwise Mutual Information

- $i(x;y) = h(x) - h(x \vert y)$
- $i(x;y) = \ln \frac{p(x \vert y)}{p(x)}$

---

## Conditional Mutual Information

$I(X;Y \vert Z) = E_{z \in Z} [D_{KL}(p_{X,Y \vert Z}(x, y \vert z) \vert \vert p_{X,Y \vert Z}(x, y \vert z) \vert \vert p_{X \vert Z}(x \vert z) p_{Y \vert Z}(y \vert z))]$

- Z가 given일때의 상황에서, Y를 알게됨으로써 얻어낸 X의 정보량
- $I(X;Y \vert Z) = I(Y;X \vert Z)$
- $I(X;Y \vert Z) = H(X \vert Z) + H(Y \vert Z) - H(X, Y \vert Z)$
- $ I(X;Y \vert Z) - I(X;Y) > 0$일 경우
  - Synergy
- $ I(X;Y \vert Z) - I(X;Y) < 0$일 경우
  - redundancy
- Chain rule for information
  - $I(X;Y,Z) = I(X;Y) + I(X;Z \vert Y)$
  - $I(X;Y,Z) = I(X;Z) + I(X;Y \vert Z)$

---

## Inequality(참고)

- Gibbs Inequality

  $\sum_{x} p_{X}(x) \log p_{X}(x) \ge \sum_{x} p_{X}(x) \log p_{Y}(x)$

  $\sum_{x} p_{X}(x) \log \frac{p_{X}(x)}{p_{Y}(x)} \ge 0$

  

- Jensen Inequality

  함수 $f$가 볼록함수(convex) 이고  $p$가 X에 대한 확률함수일때

  ​	$f(\int_{ -\infty }^{\infty} g(x)p(x) dx) \ge \int_{ -\infty }^{\infty} f(g(x))p(x) dx$ 

  함수 $f$가 오목함수(concave) 이고  $p$가 X에 대한 확률함수일때

  ​	$f(\int_{ -\infty }^{\infty} g(x)p(x) dx) \le \int_{ -\infty }^{\infty} f(g(x))p(x) dx$ 

---

## KL divergence 의 성질(참고)

- ### Forward KL

  $D_{KL}(p_{tar}(x) \vert \vert p_{hyp}(x)) = \int_{-\infty}^{\infty} p_{tar}(x) \log \frac{p_{tar}(x)}{p_{hyp}(x)} dx$ 

  $= H(p_{tar}(x)) + CE(p_{tar}(x) \vert \vert p_{hyp}(x)) $

  

  - $H(p_{tar}(x))$는 모델과 관련이 없으므로,

    Forward KL을 최소화한다 = Cross Entropy를 최소화 한다는 말

    

  - 성질 

    - $p_{tar}(x)$ = 0인 x의 부분에 대해서는 $p_{hyp}(x)$가 $p_{tar}(x)$ 에 가까워지지 않을 수도 있다.

      왜냐하면 target distribution의 density가 0에 가까운 구간에 대해서, model 이 닮지 않더라도 Forward KL은 큰 패널티를 주지 않고, 0일 때는 전혀 패널티를 주지 않기 때문이다.

    - 같은 이유로 target distribution의 밀도가 낮은 구간에 비해 밀도가 높은 구간을,  model이 더 잘 근사하는 경향이 있다.

    -  zero avoiding 현상 ($p_{tar}(x)>0$ 일 때  $p_{hyp}(x) = 0$일 경우를 피한다.)
    
      

- ### Reverse KL

  $D_{KL}(p_{hyp}(x) \vert \vert p_{tar}(x)) = \int_{-\infty}^{\infty} p_{hyp}(x) \log \frac{p_{hyp}(x)}{p_{tar}(x)} dx$ 

  $= H(p_{hyp}(x)) + CE(p_{hyp}(x) \vert \vert p_{tar}(x)) $

  

  - 성질 

    - model distibution 자기 자신의 밀도가 낮은구간에서  패널티가 적고 model distribution 자기 자신의 밀도가 높은 구간에서 패널티가 크다.
  - Foward KL과 반대로 Reverse KL을 minimize할 때, $H(p_{hyp}(x))$ 도 minimize 해야된다. 따라서 $p_{hyp}(x)$은 flat하지 않으려고 할 것이다.
    - zero forcing 현상  ($p_{tar}(x)>0$ 인데도  $p_{hyp}(x) = 0$일 경우가 존재한다.)



출처 : https://wiseodd.github.io/techblog/2016/12/21/forward-reverse-kl/