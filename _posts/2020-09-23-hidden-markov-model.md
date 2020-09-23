---
layout: post
title: "hidden markov model 정리"
---




### Table of contents
- [normalization](##normalization)
- [viterbi](##viterbi)
- [baum-welch](##baum-welch)

## normalization

## viterbi

## baum-welch 


$$
\mathbb{E}_{q(Z)}[\log{p(X, Z)}]= \sum\limits_{d=1}^{D} \left(  \sum\limits_{Z_{1:T^{(d)}}} q(Z_{1:T^{(d)}}) \left(  \log{p(z_1 )}+ \sum\limits_{t=2}^{T^{(d)}}\log{p(z_{t} \vert z_{t-1})} + \sum\limits_{t=1}^{T^{(d)}}\log{p(x_{t}=o^{d}_{t} \vert z_{t})} \right)  \right)
$$


### $\pi_i$ 와 관련있는 부분

$$
\sum\limits_{d=1}^{D}  \sum\limits_{Z_{1:T^{(d)}}} q(Z_{1:T^{(d)}}) \log{p(z_1 )} = \sum\limits_{d=1}^{D} \sum\limits_{z_1} q(z_1) \log{p(z_1)} \sum\limits_{Z_{2:T^{(d)}}} q(Z_{2:T^{(d)}} \vert z_{1}) = \sum\limits_{d=1}^{D} \sum\limits_{z_1} q(z_1) \log{p(z_1)}
$$

해당 항에 largrange 제약을 추가해서 $\pi_i$로 미분한다.
$$
\forall_i, \frac{\sum\limits_{d=1}^{D}  q(z_1 = i)}{\pi_i} = \lambda_{\pi}
$$

$\lambda_{\pi} = \sum\limits_{d=1}^{D} \sum\limits_{j} q(z_1 = j)$이면 위의 조건을 만족한다.

$$
\pi_i = \frac{\sum\limits_{d=1}^{D}  q(z_1 = i)}{\sum\limits_{d=1}^{D} \sum\limits_{j} q(z_1 = j)}
$$

### $a_{ij}$ 와 관련있는 부분

$$
\sum\limits_{d=1}^{D} \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{Z_{1:T^{(d)}}} q(Z_{1:T^{(d)}}) \log{p(z_{t} \vert z_{t-1})} = \sum\limits_{d=1}^{D} \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{Z_{2:T^{(d)}}} q(Z_{2:T^{(d)}}) \log{p(z_{t} \vert z_{t-1})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}}  \sum\limits_{Z_{2:t-2}} \sum\limits_{z_{t-1}} \sum\limits_{z_{t}} \sum\limits_{Z_{t+1:T^{(d)}}} q(Z_{2:T^{(d)}}) \log{p(z_{t} \vert z_{t-1})}
$$


$$
= \sum\limits_{d=1}^{D} \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{Z_{2:t-2}} \sum\limits_{z_{t-1}} \sum\limits_{z_{t}} \sum\limits_{Z_{t+1:T^{(d)}}}  q(Z_{2:t-2}) q(z_t, z_{t-1} \vert z_{t-2}) q(Z_{t+1:T^{(d)}} \vert z_t)\log{p(z_{t} \vert z_{t-1})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{Z_{2:t-2}} q(Z_{2:t-2})\sum\limits_{z_{t-1}} \sum\limits_{z_{t}} q(z_t, z_{t-1} \vert z_{t-2}) \log{p(z_{t} \vert z_{t-1})} \sum\limits_{Z_{t+1:T^{(d)}}}q(Z_{t+1:T^{(d)}} \vert z_t)
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{z_{t-2}} \sum\limits_{z_{t-1}} \sum\limits_{z_{t}} q(z_t, z_{t-1} \vert z_{t-2}) \log{p(z_{t} \vert z_{t-1})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{z_{t-1}} \sum\limits_{z_{t}} q(z_t, z_{t-1}) \log{p(z_{t} \vert z_{t-1})}
$$



해당 항에 largrange 제약을 추가해서 $a_{ij}$로 미분한다.
$$
\forall_j, \frac{\sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}}q(z_{t-1}=i, z_{t}=j)}{a_{ij}} = \lambda_{a_i}
$$

이를 정리하면 다음과 같게 된다.
$$
a_{ij}= \frac{\sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}}q(z_{t-1}=i, z_{t}=j)}{\sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}} \sum\limits_{k} q(z_{t-1}=i, z_{t}=k)} = \frac{\sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}}q(z_{t-1}=i, z_{t}=j)}{\sum\limits_{d=1}^{D}  \sum\limits_{t=2}^{T^{(d)}}q(z_{t-1}=i)}
$$

### $b_{im}$ 와 관련있는 부분

$$
\sum\limits_{d=1}^{D} \sum\limits_{t=1}^{T^{(d)}} \sum\limits_{Z_{1:T^{(d)}}} q(Z_{1:T^{(d)}}) \log{p(x_{t} = o^{d}_{t}\vert z_{t})} = \sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}}  \sum\limits_{Z_{1:t-1}}  \sum\limits_{z_{t}} \sum\limits_{Z_{t+1:T^{(d)}}} q(Z_{1:T^{(d)}}) \log{p(x_{t} = o^{d}_{t}\vert z_{t})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}}  \sum\limits_{Z_{1:t-1}}  \sum\limits_{z_{t}} \sum\limits_{Z_{t+1:T^{(d)}}} q(Z_{1:T^{(d)}}) \log{p(x_{t} = o^{d}_{t}\vert z_{t})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}}  \sum\limits_{Z_{1:t-1}}  \sum\limits_{z_{t}} \sum\limits_{Z_{t+1:T^{(d)}}} q(Z_{1:t-1}) q(z_{t} \vert z_{t-1}) q(Z_{t+1:T^{(d)}} \vert z_t) \log{p(x_{t} = o^{d}_{t}\vert z_{t})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}} \sum\limits_{z_{t-1}} \sum\limits_{z_{t}}  q(z_{t} \vert z_{t-1}) \log{p(x_{t} = o^{d}_{t}\vert z_{t})}
$$

$$
= \sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}} \sum\limits_{z_{t}}  q(z_{t}) \log{p(x_{t} = o^{d}_{t}\vert z_{t})}
$$


해당 항에 largrange 제약을 추가해서 $b_{im}$로 미분한다.
$$
\forall_m, \frac{\sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}}q(z_{t}=i) \delta(o^{d}_{t}=m, z_{t}=i)}{b_{im}} = \lambda_{b_i}
$$

이를 정리하면 다음과 같게 된다.
$$
b_{im}= \frac{\sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}}q(z_{t}=i) \delta(o^{d}_{t}=m, z_{t}=i)}{\sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}} \sum\limits_{k} q(z_{t}=i) \delta(o^{d}_{t}=k, z_{t}=i)} = \frac{\sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}}q(z_{t}=i) \delta(o^{d}_{t}=m, z_{t}=i)}{\sum\limits_{d=1}^{D}  \sum\limits_{t=1}^{T^{(d)}} q(z_{t}=i)}
$$



EM 알고리즘에서 $q(Z)=P(Z \vert X, \theta^{old})$로 세팅하고,  이는 forward, backward algorithm을 이용해 구할 수 있다.

