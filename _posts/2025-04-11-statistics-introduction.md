---
layout: post
title: 통계학 개론
subtitle: 제2장 통계분석
author: Insung
excerpt_image: /assets/images/ADsP/probability-distribution.png
categories: [ADsP]
tags: [ADsP, Big Data, Data Science, R, 과목 IⅠⅠ 데이터 분석]
top:
---

### 목차

[제1절 통계학 개론](/adsp/2025/04/11/statistics-introduction.html)

[제2절 기초 통계 분석](/adsp/2025/04/12/basic-statistics-analysis.html)

[제3절 다변량 분석](/adsp/2025/04/13/multivariate-analysis.html)

[제4절 시계열 예측](/adsp/2025/04/14/time-series-prediction.html)

[제5절 주성분 분석](/adsp/2025/04/15/principal-component-analysis.html)

---

## 1. 통계 개요

---

## 2. 확률과 확률분포

---

### 확률(Probability)

어떤 실험의 **모든 가능한 결과들의 집합(표본공간, $S$)** 중에서, 특정 사건 ($A \subseteq S$)가 발생할 **가능성의 정도**를 나타내는 수치입니다. 확률은 항상 0과 1 사이의 실수 값이며, **표본공간에 속한 모든 가능한 사건의 확률의 합은 항상 1**입니다.

$$
0 \leq P(A) \leq 1, \quad \sum_{i=1}^{n} P(A_i) = 1 \quad \text{(모든 가능한 사건 } A_i \text{에 대하여)}
$$

**조건부 확률(Conditional Probability):**  
특정 사건 A가 발생했다는 것이 사실이라는 전제하에 또다른 사건 B가 발생할 확률을 나타낸 값으로, 0과 1 사이의 값을 갖습니다.

$$
P(B \mid A) = \frac{P(A \cap B)}{P(A)}, \quad \text{단 } P(A) > 0
$$

| 기호 | 의미 |
| --- | --- |
|$P(B \mid A)$|"A가 발생한 후 B가 발생할 확률"|
|$P(A \cap B)$|"A와 B가 **동시에** 일어날 확률"|
|$P(A)$|조건이 되는 사건 A의 확률 (분모)|

#### 독립사건(Independent Events)

확률론에서 두 사건 A와 B는 **서로 독립(independent)**이라고 할 수 있는 조건은 다음과 같습니다.
**한 사건의 발생 여부가 다른 사건의 확률에 아무런 영향을 미치지 않아야** 합니다. 즉, A가 일어났다는 사실을 알아도 B가 일어날 확률이 **변하지 않아야** 독립입니다.

**정의 (Definition):**  
두 사건 A와 B가 **독립**일 필요충분조건은 다음과 같습니다:

$$
	P(A \cap B) = P(A) \cdot P(B)
$$

이는 "A와 B가 동시에 일어날 확률"이, "A가 일어날 확률과 B가 일어날 확률"의 **곱과 같을 때** 두 사건이 독립이라는 것을 의미합니다. 

또는 **조건부 확률**을 사용한 표현으로 다음과 같습니다:

$$
	P(B \mid A) = P(B) \quad \text{및} \quad P(A \mid B) = P(A)
$$

#### 배반사건 (Metually Exclusive Events)

확률론에서 두 사건 A와 B가 **배반(mutually exclusive)**이라고 할 때는, **둘 중 하나라도 발생하면 나머지는 절대 발생하지 않음**을 의미합니다. 즉, 두 사건은 **동시에 일어날 수 없습니다.**

**정의 (Definition):**

두 사건 A와 B는 **배반 사건**일 때 다음 조건을 만족합니다.

$$
	P(A \cap B) = 0
$$

이는 "A와 B가 동시에 발생할 확률"이 0이라는 뜻이며, **서로 겹치는 경우가 없음**을 의미합니다.

또한, A와 B가 배반이라면, 둘 중 하나라도 발생할 확률은 다음과 같이 계산 됩니다:

$$
	P(A \cup B) = P(A) + P(B)
$$
이는 두 사건이 겹치지 않기 때문에, 단순히 각 확률을 **더하면 전체 확률**이 된다는 뜻입니다.

#### 확률변수(Random Variable)
확률변수는 확률 실험의 **결과를 수치로 표현하는 함수**입니다. 즉, 표본공간 $ \Omega $의 각 결과에 **수치적인 값을 대응시키는 함수**로서, 단순한 숫자가 아니라, 불확실한 실험 결과를 수학적으로 수치화한 함수입니다. 관측되는 데이터 값은 확률변수의 **실현값(realisaition)**입니다. 

**정의 (Definition):**

> A random variable is a function that assigns a real number to each outcome in a sample space:  
> -> 확률변수는 표본공간의 각 결과에 하나의 실수 값을 대응시키는 함수입니다.

$$
	X : \Omega \rightarrow \mathbb{R}
$$
- $\Omega$: 표본공간 (Sample Space)
- $X$: 확률변수
- $\mathbb{R}$: 실수 집합


#### 확률분포 (Probability Distribution)

확률분포는 확률변수가 어떤 값을 가질 수 있으며, 그 각각의 값 혹은 구간에 **어떤 확률이 할당되는지**를 설명하는 수학적 규칙입니다. 확률변수가 이산형 혹은 연속형이냐에 따라 정의 방식이 달라집니다. 확률분포는 확률변수의 전체 행동을 설명하는 구조이며, 값의 분포 특성, 경향성, 불확실성의 형태를 모두 포함합니다.

**표현식:**

- 이산형:
$$
	\sum_i P(X = x_i) = 1
$$

- 연속형:
$$
	\int_{-\infty}^{\infty} f_X(x)\, dx = 1
$$

![Probability Distribution](/assets/images/ADsP/probability-distribution.png)

#### 확률함수 (Probability Distribution)
확률함수는 확률변수의 값에 확률 또는 확률밀도를 할당하는 함수로, 이는 확률분포를 수학적으로 표한하는 도구 입니다. 확률변수의 유형에 따라 함수의 성격이 달라집니다.

**정의 (Definition):**

> A probability function defines the likelihood that a random variable takes on specific values or falls within a giveen range.

즉, 확률함수는 확률변수의 값에 **얼마만큼 확률이 할당되는지를 수치적으로 기술하는 함수**입니다.

**분류 (Types of Random Variables):**

1. 확률질량함수(Probability Mass Functionm, PMF)
- 이산 확률변수에 사용
- 각 가능한 값 $x$에 대해 확률 $P(X = x)$를 반환 

$$
	P(X = x), \quad \sum_x P(X = x) = 1
$$

2. 확률밀도함수(Probability Density Function, PDF)
- 연속 확률변수에 사용 
- 특정 값의 확률은 0이며, 구간에 대한 확률로 표현 

$$
	P(a \leq X \leq b) = \int_a^b f_X(x)\, dx, \quad \int_{-\infty}^{\infty} f_X(x)\, dx = 1
$$

> 기대값 (Expected Value)
> - 이산형:  
> $\mathbb{E}[X] = \sum_x x \cdot P(X = x)$
> - 연속형:  
> $\mathbb{E}[X] = \int_{-\infty}^{\infty} x \cdot f_X(x)\, dx$  

> 분산 (Variance)  
> $\operatorname{Var}(X) = \mathbb{E}[(X - \mathbb{E}[X])^2]$

