---
layout: post
title: 기초 통계 분석
subtitle: 제2장 통계분석
author: Insung
excerpt_image: /assets/images/ADsP/probability-distribution.png
categories: [ADsP]
tags: [ADsP, Big Data, Data Science, R, 과목 IⅠⅠ 데이터 분석]
top:
---

### 목차

[제1절 통계학 개론](/adsp/2025/04/11/statistics-introduction.html)

[제2절 기초 통계 분석](/adsp/2025/04/13/basic-statistics-analysis.html)

- [t-검정](/adsp/2025/04/13/basic-statistic-analysis.html)

- [분산분석(ANOVA)](/adsp/2025/04/13/anova.html)

[제3절 다변량 분석](/adsp/2025/04/14/multivariate-analysis.html)

[제4절 시계열 예측](/adsp/2025/04/15/time-series-prediction.html)

[제5절 주성분 분석](/adsp/2025/04/16/principal-component-analysis.html)

---

## 1. t-검정(t-test)

---

### 일 표본 t-검정(one-sample t-test)
일(단일) 표본 t-검정은 하나의 표본이 어떤 기준값(모집단)과 통계쩍으로 유의한 차이가 있는지 평가하는 가설 검정 방법입니다. 이 검정은 모집단의 분산(또는 표준편차)을 알수 없고, 표본 데이터를 통해 모평균을 추청해야 할 때 사용됩니다.

#### 일 표본 단측 t-검정(one-sample one-tailed t-test)
단측 검정은 대립가설이 특정 방향성을 가질 때 사용합니다. 즉, 모평균이 특정 값보다 **크다** 또는 **작다**는 방향성이 포함된 경우입니다. 
예를들어, 다음과 같은 가설을 수립할 수 있습니다:
- **귀무가설 $H_0$:** 지우개의 평균 중량은 50g 이하이다.   $(\mu \leq 50)$
- **대립가설 $H_1$:** 지우개의 평균 중량은 50g을 초과한다.  $(\mu > 50)$

이러한 경우, 단측 t-검정을 통해 표본 평균이 50g보다 통계적으로 유의하게 큰지를 평가합니다. 검정 통계량은 다음과 같이 계산됩니다: 
$$
t = \frac{\bar{x} - \mu_0}{\frac{s}{\sqrt{n}}}
$$
- $\bar{x}$: 표본 평균
- $\mu_0$: 비교 대상 모평균 (예: 50g)
- $s$: 표본 표준편차
- $n$: 표본 크기



```R
# 일 표본 단측 t-검정을 위한 지우개 10개의 표본추출
weights <- runif(10, min = 49, max = 52)
t.test(weights, mu = 50, alternative = 'greater') # 반대 방향은 'less'를 사용
```


    
    	One Sample t-test
    
    data:  weights
    t = 2.5763, df = 9, p-value = 0.01494
    alternative hypothesis: true mean is greater than 50
    95 percent confidence interval:
     50.17174      Inf
    sample estimates:
    mean of x 
     50.59536 



- t-value(검정 통계량): 표본 평균이 모평균(귀무가설 평균)보다 얼마나 멀리 떨어졌는지(표준 오차 단위로) 표현
- df(자유도): 표본크기 10 -> n - 1 = 9
- p-value(유의확률): 귀무가설 하에서 **이 정도 평균 이상**이 나올 확률
- significance level(유의수준): 귀무가설을 기각하기 위한 기준값이며, 일반적으로 5%(0.05)로 설정됩니다.
- p-value가 유의수준 0.05보다 작으므로 귀무가설을 기각할 수 있는 통계적 근거가 있습니다.

> 즉, "이번 결과는 통계적으로 유의미하므로, 단순한 변동이나 우연으로 보기 어렵습니다. 따라서 기존 평균과는 통계적으로 의미 있는 차이가 있다고 판단할 수 있습니다."

#### 일표본 양측 t-검정(one-sample two-tailed t-test)
일표본 양측 t-검정은 단일 표본이 주어진 기준 평균값과 **통계적으로 유의한 차이가 있는지(크거나 작음 모두 포함)** 를 판단하는 가설 검정 방법입니다. 이 검정은 모집단의 분산을 알 수 없고, 표본 분산으로 추정하며 정규성을 가정하는 상황에서 사용합니다. 즉 표본이 기준 평균값과 같지 않다는 주장을 검정하는 경우 사용하며, 방향성은 따지지 않습니다.


```R
# 일 표본 양측 t-검정을 위한 40kg ~ 100kg 사이 남성 100명의 표본을 추출
weights <- runif(100, min = 40, max = 100)
t.test(weights, mu = 70, alternative = 'two.sided')
```


    
    	One Sample t-test
    
    data:  weights
    t = -0.29899, df = 99, p-value = 0.7656
    alternative hypothesis: true mean is not equal to 70
    95 percent confidence interval:
     66.12719 72.85852
    sample estimates:
    mean of x 
     69.49285 



- 검정 통계량(t-value)은 `–0.299`, 자유도는 `99`이며, p-value는 `0.766`으로 유의수준 0.05보다 훨씬 큽니다.
- 이는 관측된 표본 평균(69.49)이 귀무가설의 기준값(70)과 통계적으로 유의한 차이가 없음을 나타냅니다.

> 즉, "이번 결과는 단순한 랜덤 변동 또는 우연으로 발생했을 가능성이 높으며, 귀무가설을 기각할 수 있는 통계적 근거가 부족합니다. 따라서 모집단의 평균은 70과 다르다고 보기 어렵습니다."


### 독립 이표본 t-검정(independent sample t-test)
독립 이표본 t-검정은 **두 개의 독립적인 표본**이 서로 **같은 모집단 평균을 가지는지 여부**를 통계적으로 평가하는 가설 검정 방법입니다. 이 검정은 두 집단 간의 평균 차이가 **우연에 의한 것인지**, 아니면 **실제로 유의한 차이가 존재하는지**를 판단할 때 사용됩니다. 모집단의 분산이 알려져 있지 않으며, 두 표본의 분산을 이용해 검정 통계량을 추정합니다. 이때, **두 모집단의 분산이 동일하다고 가정하는 경우**에는 Student의 t-검정(pooled t-test) 을, **분산이 다를 수 있다고 판단되는 경우**에는 **Welch의 t-검정**을 사용합니다. 실무에서는 분산의 동질성을 사전에 확인하기 위해 **등분산 검정(F-test 또는 Levene's test)** 을 수행할 수 있으나, 표본 크기나 분산이 다를 가능성을 고려해 기본적으로 **Welch의 t-검정**을 사용하는 것이 권장됩니다.

#### 단측 vs 양측 이표본 검정
- **단측 검정(One-Tailed):** 두 집단 중 하나가 더 크다/작다는 방향성을 검정
- **양측 검정(Two-Tailed):** 두 집단 간 차이 존재 여부를 검정(방향성 무관)

#### 이 표본 단측 t-검정(independent one-tailed t-test)  

예를 들어, A 집단의 평균이 B 집단보다 작은지 검정하고자 한다면 다음과 같은 가설을 수립합니다:

- **귀무가설 $H_0$:** A 집단의 평균은 B 집단보다 같거나 크다.   $(\mu_1 \geq \mu_2)$
- **대립가설 $H_1$:** A 집단의 평균이 B 집단보다 작다.        $(\mu_1 < \mu_2)$

등분산을 가정하는 경우 (pooled t-test), 검정 통계량은 다음과 같이 계산됩니다:

$$
t = \frac{\bar{x}_1 - \bar{x}_2}{s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}
$$
$$
s_p = \sqrt{ \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2} }
$$

- $\bar{x}_1$, $\bar{x}_2$: 두 집단의 표본 평균
- $s_1$, $s_2$: 두 집단의 표본 표준편차
- $n_1$, $n_2$: 표본 크기
- $s_p$: 공통 표준편차 (pooled standard deviation)

※ 분산이 같다고 가정할 수 없다면 Welch의 t-검정을 사용해야 합니다.


```R
# 이 표본 단측 t-검정을 위해 각 집단별로 100개씩 표본추출
salaryA <- runif(100, min = 250, max = 390)
salaryB <- runif(100, min = 280, max = 400)
t.test(salaryA, salaryB, alternative = 'less')
```


    
    	Welch Two Sample t-test
    
    data:  salaryA and salaryB
    t = -3.5351, df = 192.27, p-value = 0.0002553
    alternative hypothesis: true difference in means is less than 0
    95 percent confidence interval:
          -Inf -9.802698
    sample estimates:
    mean of x mean of y 
     320.0464  338.4566 



- 검정 통계량(t-value)은 `-3.535`, 자유도는 `192.27`, p-value는 `0.00026`으로 유의수준 0.05보다 **현저히 작습니다.**
- 이는 관측된 두 집단 간 평균 차이가 단순한 우연으로 발생했을 가능성이 매우 낮으며, A 집단의 평균이 B 집단보다 통계적으로 유의하게 작다는 사실을 지지합니다.

> 즉, "이번 결과는 귀무가설을 강하게 기각할 수 있는 통계적 근거를 제공하며, A 집단의 평균이 B 집단보다 **유의하게 낮은 수준**임을 시사합니다. 이러한 차이는 우연에 의한 결과라 보기 어렵고, **실질적인 모집단 간 차이**가 존재한다고 판단할 수 있습니다."


#### 독립 이표본 양측 t-검정(Independent Two-Sample Two-Tailed t-Test)
예를 들어, K 집단의 평균 달리기 속도가 L 집단과 **다른지** 검정하고자 할 경우 다음과 같이 가설을 수립합니다:

- **귀무가설 $H_0$:** 두 집단의 평균은 같다.   $(\mu_1 = \mu_2)$
- **대립가설 $H_1$:** 두 집단의 평균은 다르다.  $(\mu_1 \neq \mu_2)$


```R
# 이 표본 양측 t-검정을 위해 각 집단별로 100개씩 표본추출
speedK <- runif(100, min = 30, max = 40)
speedL <- runif(100, min = 25, max = 35)
t.test(speedK, speedL, alternative = 'two.sided')
```


    
    	Welch Two Sample t-test
    
    data:  speedK and speedL
    t = 12.032, df = 198, p-value < 2.2e-16
    alternative hypothesis: true difference in means is not equal to 0
    95 percent confidence interval:
     4.054320 5.643768
    sample estimates:
    mean of x mean of y 
     34.93825  30.08921 



- 검정 통계량(t-value)은 `12.032`, 자유도(df)는 `198`, p-value는 `< 2.2e-16`으로 유의수준 0.05보다 **압도적으로 작습니다.**
- 이는 두 집단의 평균 속도 차이가 **우연히 발생했을 가능성이 거의 없으며,** 통계적으로 매우 **유의한 차이**가 존재함을 나타냅니다.

> 이번 검정 결과는 귀무가설(두 집단의 평균 속도가 동일하다는 가정)을 **강하게 기각할 수 있는 통계적 근거**를 제공합니다. **K 집단은 L집단 보다 평균적으로 유의하게 빠른 속도를 보였으며**, 이러한 차이는 우연이 아닌 실질ㅈ거인 모집단 차이로 해석할 수 있습니다.

### 대응 표본 t-검정(Paired t-test)
대응 표본 t-검정은 동일한 개체나 유사한 쌍(pair)에 대해 두 시점 또는 두 조건에서 측정된 값을 비교하여, 평균 차이가 **통계적으로 유의한지** 검정하는 방법입니다. 이 검정은 두 데이터가 **쌍을 이루며 종속된 구조**를 가질 때 사용됩니다. 

보통 다음과 같은 경우에 적용됩니다: 
- 한 집단의 **처치 전 vs 후 효과 비교** (예: 약 복용 전후 혈압)
- 동일 대상의 **시간에 따른 변화 측정** (예: 정책 시행 전후 가격 변화)
- 짝지어진 두 조건 간의 비교 (예: 좌·우 눈의 시력 등)

#### 대응 표본 단측 t-검정
새로운 운동법이 체중 감량에 효과가 있는지를 검증하기 위해, 운동 전과 운동 후의 체중을 비교하고자 할 때 대응 표본 단측 t-검정을 수행할 수 있습니다. 이때 운동 후 체중이 운동 전보다 유의하게 감소했는지를 확인하려는 목적이라면, 다음과 같이 가설을 설정합니다:

- 귀무가설 $H_0$: 운동 후 체중은 운동 전보다 **같거나 더 무겁다.**  $(\mu_d \leq 0)$
- 대립가설 $H_1$: 운동 후 제충은 **유의하게 감소했다.**  $(\mu_d > 0)$  
→ 여기서 $\mu_d = \mu_{\text{before}} - \mu_{\text{after}}$



```R
# 단측 대응 표본 t-검정을 위한 표본추출
before <- runif(10, min = 60, max = 80)
after <- before + rnorm(10, mean = -3, sd = 2)
t.test(before, after, alternative = 'greater', paired = TRUE)
```


    
    	Paired t-test
    
    data:  before and after
    t = 4.1742, df = 9, p-value = 0.001198
    alternative hypothesis: true mean difference is greater than 0
    95 percent confidence interval:
     1.77135     Inf
    sample estimates:
    mean difference 
           3.158321 



- 검정 통계량(t-value)은 `4.174`, 자유도(df)는 `9`, p-value는 `0.0012`로 유의수준 0.05보다 **현저히 작습니다.**
- 평균 차이는 `3.16`으로 운동 전보다 후에 평균적으로 약 3.16kg 감소, 신뢰구간 `95%`에 차이는 최소 `1.77`이상 감소했을 가능성이 높습니다.
- 이는 두 시점 간 평균 차이가 **우연히 발생했을 가능성이 매우 낮으며**, 통계적으로 유의한 감소 효과가 존재함을 의미합니다.

> 이번 분석 결과 **운동 전후 체중 차이가 단순한 우연이 아닌 통계적으로 유의한 변화**임을 보여줍니다. 귀무가설(운동 전후 체중에 차이가 없다)을 기각할 수 있는 충분한 통계적 근거가 있으며, **운동 후 체중은 유의하게 감소한 것**으로 판단됩니다. 이는 운동 프로그램이 체중 감량에 **실질적인 효과가 있었음을 시사**합니다.