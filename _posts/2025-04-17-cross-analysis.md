---
layout: post
title: 교차분석
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

- [교차분석](/adsp/2025/04/17/cross-analysis.html)

- [상관분석](/adsp/2025/04/17/correlation-analysis.html)

- [회귀분석](/adsp/2025/05/01/regression-analysis.html)

[제3절 다변량 분석](/adsp/2025/04/14/multivariate-analysis.html)

[제4절 시계열 예측](/adsp/2025/04/15/time-series-prediction.html)

[제5절 주성분 분석](/adsp/2025/04/16/principal-component-analysis.html)

---

## 3. 교차분석(Cross Tabulation Analysis)

---

교차분석은 **두 개 이상의 범주형 변수(categorical variables)**간의 관계를 탐색하기 위한 분석 기법입니다. 각 범주 조합에 대한 **빈도(frequency)**를 테이블 형태로 정리하여, 변수 간의 **연관성(association)** 또는 **독립성(independence)**을 시각적으로 확인하고, 필요 시 **카이제곱 검정(χ² test)**을 사용해 통계적으로 감정합니다.

#### 사용 목적 및 검정 유형
| 검정 종류 | 목적 |
| ------- | --- |
|적합도 검정(Goodness-of-Fit)|관측된 분포가 이론적 기대 분포와 얼마나 일치하는지 검정|
|독립성 검정(Test of Independence)|두 범주형 변수 간의 독립 여부를 검정|
|동질성 검정(Test of Homogeneity)|서로 다른 집단의 분포가 동일한지 비교|

#### 교차분석표(Crosstab Table)
두 개 이상의 **범주형 변수 간의 조합별 빈도수(frequency)**를 **행렬 형태**로 나타낸 표입니다. 이는 **독립성 검정(카이제곱 검정)**이나 **연관성 분석**의 **기초 데이터 구조**로 사용됩니다.

**지역별 전자제품 브랜드 선호도**
|   | A사 | B사 | C사 | 계 |
| - | --- | --- | --- | --- |
| 한국 | 30 | 55 | 15 | 100 |
| 미국 | 40 | 60 | 20 | 120 |
| 유럽 | 40 | 35 | 15 | 90 |
| 계 | 110 | 150 | 50 | 300 |

- 이 교차표를 통해 지역별 선호 브랜드 경향의 차이를 시각적으로 파악할 수 있으며, 카이제곱 독립성 검정을 통해 '지역'과 '브랜드 선호도'가 독립적인 변수인지 아닌지를 검정할 수 있습니다.

### 적합도 검정(Goodness-of-Fit Test) 
적합도 검정은 실제 데이터(관측도수)가 특정한 이론적 분포 또는 기대 분포(예: 균등분포, 정규분포 등)와 **얼마나 잘 부합하는지**를 검정하는 방법입니다. 이는 모집단에 대한 가설(예: 브랜드 선호가 균등하게 분포할 것이다)이 **실제 데이터에 적절한지 여부를 판단**하는 데 사용됩니다. 실험 결과 관측도수가 기대도수와 일치하면 실제 분포와 예측 분포 간에는 차이가 없다고 불 수 있습니다.

| 용어 | 의미 |
| --- | --- |
|관측도수(Observed Frequency)|실제 데이터로 측정된 값|
|기대도수(Expected Frequency)|이론적 분포나 가설에 따라 기대되는 값|
|카이제곱 통계량(chi-squared Statistic)|관측값과 기대값 사이의 차이를 수치화한 값|

#### 검정 통계량
$$ 
\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}
$$ 

- $O_i$: i번째 범주의 관측도수 (Observed)
- $E_i$: i번째 범주의 기대도수 (Expected)
- 모든 범주에 대해 차이의 제곱을 기대도수로 나누어 합산


#### 해석 방법
- χ² 통계량이 클수록 관측값과 기대값 간의 차이가 큼 -> 가설이 부적절할 가능성 증가
- p-value < 0.05 -> 기대 분포와 관측 분포 간에 **통계적으로 유의한 차이 있음** -> 귀무가설 기각
- p-value ≥ 0.05 -> 기대 분포와 관측 분포 간의 차이가 **통계적으로 유의하지 않음** -> 귀무가설 유지
  m

```R
# 귀무가설(H₀): 세 브랜드는 동일하게 선호된다 (균등 분포 1:1:1)
# 대립가설(H₁): 세 브랜드 중 선호에 차이가 있다.

# 관측도수 입력 
observed <- c(25, 40, 35)

# 기대도수 생성 (총합은 자동 계산됨) 
expected <- rep(100 / 3, 3) # 균등 분포 가정

# 적합도 검정 수행
result <- chisq.test(x = observed, p = c(1/3, 1/3, 1/3))

# 결과 출력
print(result)
```

    
    	Chi-squared test for given probabilities
    
    data:  observed
    X-squared = 3.5, df = 2, p-value = 0.1738
    


- 유의수준(0.05)보다 p-value가 크므로 귀무가설을 기각하지 않습니다.
- 관측된 브랜드 선호도는 균등 분포와 통계적으로 유의한 차이가 없습니다.

> 즉, 세 브랜드는 동일하게 선호된다고 볼 수 있습니다.

### 독립성 검정(Test of Independence)
독립성 검정은 두 개의 **범주형 변수(categorical variables)**간에 **통계적으로 유의미한 관계가 존재하는지**를 검정 하는 방법입니다. 가장 일반적으로는 **카이제곱 검정(Chi-squared Test)**이 사용되며, 두 변수 간의 **독립성(independence)** 또는 **연관성(association)** 여부를 평가합니다.

#### 목적
| 목적 | 설명 |
| --- | --- |
|두 범주형 변수 간의 독립 여부 검정|예: 성별과 투표 성향이 무관한지|
|변수 간 연관성 확인|마케팅, 의료, 사회과학 등에서 범주형 변수 간 관계 분석| 
|데이터 기반 가설 검정|관측된 데이터가 귀무가설(독립)을 따르는지 판단| 

#### 전제 조건
- 데이터는 **관측 빈도(frequency data)**여야 함(연속형 변수는 부적절)
- 각 셀의 **기대도수(Expected frequency)**는 일반적으로 **5 이상**이어야 함 (소표본일 경우 Fisher's Exact Test 권장)
- 독립 표본이어야 하며, 각 관측치는 중복되지 않아야 함

#### 검정 통계량
$$ 
\chi^2 = \sum \frac{(O_ij - E_ij)^2}{E_ij}
$$ 

- $O_ij$: 관측도수 (Observed frequency)
- $E_ij$: 기대도수 (Expected frequency)

-> 모든 셸에 대해 계산하여 **카이제곱 통계량** 도출


```R
# 교차표 생성 (지역별 x 브랜드 선호도)
brand_table <- matrix(c(30, 55, 15,
                        40, 60, 20,
                        40, 35, 15),
                      nrow = 3,
                      byrow = TRUE)

# 행과 열 이름 설정
rownames(brand_table) <- c("한국", "미국", "유럽")
colnames(brand_table) <- c("A사", "B사", "C사")

# 교차표 출력
print(brand_table)

# 독립성 검정 수행
result <- chisq.test(brand_table)

# 결과 출력
print(result)
```

         A사 B사 C사
    한국  30  55  15
    미국  40  60  20
    유럽  40  35  15
    
    	Pearson's Chi-squared test
    
    data:  brand_table
    X-squared = 5.8034, df = 4, p-value = 0.2143
    


- 카이제곱 통계량 = `5.8034`, 자유도(df) = `4`, p-value = `0.2143`
- p-value가 유의수준 0.05보다 크므로 귀무가설을 기각할 수 없음 

> 즉, 현재 데이터에서는 지역과 전자제품 브랜드 선호 사이에 유의한 통계적 연관성이 없다. 따라서, 지역에 따른 브랜드 선호 차이는 우연으로 볼 수 있는 수준이다.

### 동질성 검정(Test of Homogeneity)
동질성 검정은 두 개 이상의 **독립된 집단(independent groups)**이 **동일한 분포(또는 비율 분포)**를 가지는지를 검정하는 방법입니다. 주로 **여러 집단 간 범주형 변수의 분포가 동일한지**를 평가하며, **카이제곱 검정(Chi-squared Test)**을 사용합니다. 

독립성 검정과는 유사한 수식을 사용하지만, 샘플링 방식과 해석의 초점이 다릅니다. 

#### 목적
| 목적 | 설명 |
| --- | --- |
| 여러 집단 간 분포의 동일성 검정 | 예: 국가별 브랜드 선호 분포가 같은가? | 
| 정책/시장/임상 집단 간 차이 유무 확인 | 예: 병원별 치료 결과 분포가 동일한가? |
| 통계적 집단 비교 기반 | 독립된 표본을 통해 각 집단 간 구조적 차이를 평가 |

#### 전제 조건
- 각 집단은 **서로 독립된 표본**이어야 함
- 데이터는 **빈도 데이터(categorical freqeuncy)**여야 함
- 각 셀의 **기대도수(Expected frequency)**는 **5 이상**이 권장됨

-> 기대도수가 작으면 **Fisher's Exact Test** 또는 **p-value 시뮬레이션** 고려

#### 검정 통계량
$$
\chi^2 = \sum \frac{(O_{ij} - E_{ij})^2}{E_{ij}}
$$
- $O_{ij}$: 관측도수 (Observed frequency)
- $E_{ij}$: 기대도수 (Expected frequency)

→ 집단 간 분포 차이가 없다는 귀무가설 하에서, 기대되는 이론값과 관측값의 차이를 기반으로 카이제곱 통계량 도출


```R
# 교차표 생성 (지역별 x 브랜드 선호도)
brand_table <- matrix(c(30, 55, 15,
                        40, 60, 20,
                        40, 35, 15),
                      nrow = 3,
                      byrow = TRUE)

# 행과 열 이름 설정
rownames(brand_table) <- c("한국", "미국", "유럽")
colnames(brand_table) <- c("A사", "B사", "C사")

# 동질성 검정 (카이제곱 검정)
result <- chisq.test(brand_table)

# 결과 출력
print(result)

# 기대도수 확인
result$expected
```

    
    	Pearson's Chi-squared test
    
    data:  brand_table
    X-squared = 5.8034, df = 4, p-value = 0.2143
    



<table class="dataframe">
<caption>A matrix: 3 × 3 of type dbl</caption>
<thead>
	<tr><th></th><th scope=col>A사</th><th scope=col>B사</th><th scope=col>C사</th></tr>
</thead>
<tbody>
	<tr><th scope=row>한국</th><td>35.48387</td><td>48.38710</td><td>16.12903</td></tr>
	<tr><th scope=row>미국</th><td>42.58065</td><td>58.06452</td><td>19.35484</td></tr>
	<tr><th scope=row>유럽</th><td>31.93548</td><td>43.54839</td><td>14.51613</td></tr>
</tbody>
</table>



**해석**
- 귀무가설(H₀): 세 지역의 브랜드 선호 분포는 동일하다
- 대립가설(H₁): 지역 간 브랜드 선호 분포는 동일하지 않다
- p-value = 0.2143 > 0.05 → 귀무가설 기각 불가

> 결론: 통계적으로 세 지역은 동일한 선호 분포를 가진다고 볼 수 있습니다.

#### 중심극한정리Central Limit Theorem, CLT)
**중심극한정리**는 통계학에서 가장 중요한 이론 중 하나로, 표본을 통해 모집단의 특성을 추정할 수 있게 해주는 수학적 기반을 제공합니다. 중심극한정리는 다음과 같은 내용을 포함합니다:

**모집단의 분포 형태와 관계없이**, 표본의 크기 `n`이 충분히 크다면, 동일한 크기의 표본을 여러 번 반복 추출해 계산한 **표본 평균들의 분포는 정규분포에 근사하게 수렴**한다.

이는 모집단이 비정규분포이거나 왜도(skewness)를 갖는 분포라고 해도, 표본평균의 분포는 일정 조건을 만족할 경우 정규분포와 유사한 형태를 나타낸다는 점에서 매우 유용합니다.

**표본평균분포란?**
- 여기서 말하는 '표본평균분포'는 단일 표본에서 계산된 평균값을 의미하는 것이 아니라, 모집단으로부터 **동일한 크기 $n$**의 표본을 **여러 번 반복 추출**했을 때, **각 표본에서 구한 평균값들로 구성된 분포**를 말합니다.
- 주의할 것은 표본의 크기가 아무리 크다 해도 단 하나의 표본집단의 평균이 모집단의 평균과 같아지는 것은 아닙니다. 왜냐하면 표본은 매번 추출할 때마다 달라지고, 표본 평균 역시 일정한 오차를 포함합니다.

결론적으로 중심극한정리는 **'표본평균의 분포는 정규분포로 수렴한다'**는 성질을 통해 모집단이 어떤 분포를 따르든지간에, 충분히 큰 표본을 통해 정규분포 기반의 통계 추론이 간으함을 수학적으로 보장해줍니다.


```R

```
