---
layout: post
title: 빅데이터 분석 방법론
subtitle: 제1장 데이터 분석 기획의 이해
author: Insung
categories: [ADsP]
tags: [ADsP, Big Data, Data Science, 과목 IⅠ 데이터 분석 기획]
top:
---

### 목차

[제1절 분석 기획 방향성 도출](/adsp/2025/03/31/analysis-planning-direction.html)

[제2절 분석 방법론](/adsp/2025/04/01/analysis-methodology.html)

[제2-1절 빅데이터 분석 방법론](/adsp/2025/04/02/big-data-analysis-methodology.html)

[제3절 분석 과제 발굴](/adsp/2025/04/01/analysis-task-discovery.html)

[제4절 분석 프로젝트 관리 방안](/adsp/2025/04/02/project-management-plan.html)

---

## 1. 빅데이터 분석 방법론 개요

---

**빅데이터 분석 방법론(Big Data Analysis Methodology)**

빅데이터 분석 방법론은 완벽한 계층적 프로세스 모델로서 단계, 태스크, 스텝의 3계층 레벨과 5단계로 구성되어 있습니다. 5개의 단계들을 프로세스 그룹이라 하며, 각 단계는 여러 개의 태스크로 구성되는데 각 태스크는 물리적 또는 논리적으로 품질 검토의 항목이 될 수 있습니다. 마지막 계층인 스텝은 입력자료, 출력 및 도구, 출력자료 등으로 구성된 단위 프로세스들 입니다.

**빅데이터 분석 방법론의 계층적 프로세스**

빅데이터 분석 방법론은 분석 기획, 데이터 준비, 데이터 분석, 시스템 구현, 평가 및 전개의 5개 단계와 각각의 태스크와 스텝이 순차적으로 진행되며, 필요에 따라 데이터 준비 단계와 데이터 분석 단계가 피드백을 주고받을 수 있습니다. 


![Big Data Analysis Methodology](/assets/images/ds/bigdata-hierarchical-process.png)


### 빅데이터 분석 방법론 단계별 상세화 (태스크 및 스텝 포함)

빅데이터 분석 방법론의 각 단계를 태스크와 스텝으로 상세화하여 체계적인 분석 프로세스를 구축할 수 있습니다. 아래는 각 단계를 태스크와 스텝으로 분해한 예시입니다.

#### Phase 1 분석 기획 (Analysis Planning)

- **Task 1 비즈니스 이해 및 범위 설정 (Business Understanding & Scope Setting)**
    - Step 1.1 비즈니스 이해(문제 정의) (Business Problem Definition): 분석 대상인 업무 도메인에 대한 이해
        - 입력 자료: 비즈니스 요구사항, 문제 정의서
        - 처리 및 도구: 인터뷰, 워크숍, 문서 분석
        - 출력 자료: 명확하게 정의된 비즈니스 문제
    - Step 1.2 프로젝트 범위 설정 (Project Scope Definition): 프로젝트 목적에 부합하는 범위를 설정
        - 입력 자료: 정의된 비즈니스 문제, 가용 자원
        - 처리 및 도구: 범위 정의 회의, 요구사항 분석
        - 출력 자료: 프로젝트 범위 정의서(SOW, Statement Of Work)<br>
<br>

- **Task 2 프로젝트 정의 및 계획 수립 (Project Definition & Planning)**
    - Step 2.1 데이터 분석 프로젝트 정의 (Data Analysis Project Definition): 프로젝트 목표를 명확히 하기 위한 평가 기준을 설정
        - 입력 자료: 프로젝트 범위 정의서, 분석 목표
        - 처리 및 도구: 분석 방법론 선택, 프로젝트 목표 설정, 모델 운영 이미지 설계
        - 출력 자료: 데이터 분석 프로젝트 정의서, 모델 운영 이미지 설계서
    - Step 2.2 프로젝트 수행 계획 수립 (Project Execution Plan): 프로젝트 목적, 기대효과 프로젝트 관리방안 등 프로젝트 수행 계획서 작성
        - 입력 자료: 데이터 분석 프로젝트 정의서, 가용 자원, 모델 운영 이미지 설계서
        - 처리 및 도구: 일정 관리, 자원 할당, 커뮤니케이션 계획
        - 출력 자료: 프로젝트 수행 계획서, WBS(Work Breakdown Structure)<br>
<br>

- **Task 3 프로젝트 위험 계획 수립 (Project Risk Planning)**
    - Step 3.1 데이터 분석 위험 식별 (Data Analysis Risk Identification): 프로젝트 진행 시 발생 가능한 위험 식별
        - 입력 자료: 프로젝트 범위 정의서, 프로젝트 수행 계획서, 과거 프로젝트 경험(선행 프로젝트 산출물)
        - 처리 및 도구: 위험 식별 회의, 위험 분석 도구, 위험 우선순위 판단
        - 출력 자료: 위험 식별 목록
    - Step 3.2 위험 대응 계획 수립 (Risk Response Plan): 식별된 위험에 대한 분석을 통하여 대응 방안을 수립
        - 입력 자료: 위험 식별 목록, 위험 평가 결과, 프로젝트 정의서, 프로젝트 수행 계획서
        - 처리 및 도구: 위험 대응 (정량적, 정성적) 전략 수립, 비상 계획 수립
        - 출력 자료: 위험 대응 관리 계획서

#### Phase 2 데이터 준비 (Data Preparation)

- **Task 1 필요 데이터 정의(Required Data Definition)**
    - Step 1.1 필요 데이터 정의 (Required Data Definition): 다양한 데이터 소스로부터 필요 데이터 정의
        - 입력 자료: 프로젝트 수행 계획서, 시스템 설계서, ERD, 메타데이터 정의서
        - 처리 및 도구: 데이터 요구사항 분석, 데이터 정의서 작성
        - 출력 자료: 데이터 정의서
    - Step 1.2 데이터 획득 방안 수립 (Data Acquisition Plan): 데이터 수집하기 위한 구체적인 방안을 수립
        - 입력 자료: 데이터 정의서, 시스템 설계서
        - 처리 및 도구: 데이터 획득 방안 수립
        - 출력 자료: 데이터 획득 계획서<br>
<br>

- **Task 2 데이터 스토어 설계 (Data Store Design)**
    - Step 2.1 정형 데이터 스토어 설계(Structured Data Store Design): 데이터의 효율적인 저장과 활용을 위한 정형 데이터 스토어 설계
        - 입력 자료: 데이터 정의서, 데이터 획득 계획서
        - 처리 및 도구: 데이터베이스 설계, 데이터 모델링 도구, 데이터 매핑
        - 출력 자료: 정형 데이터 스토어 설계서, 데이터 매핑 정의서
    - Step 2.2 비정형 데이터 스토어 설계 (Unstructured Data Store Design): Hadoop, NoSQL 등 비정형 데이터 저장소 설계
        - 입력 자료: 데이터 정의서, 데이터 획득 계획서
        - 처리 및 도구: 비정형 데이터 저장소 설계 도구, 데이터 모델링 도구
        - 출력 자료: 비정형 데이터 스토어 설계서, 데이터 매핑 정의서<br>
<br>        

- **Task 3 데이터 수집 및 정합성 검정 (Data Collection & Consistency Review)**
    - Step 3.1 데이터 수집 및 저장 (Data Collection & Storage): 수집된 데이터를 설계된 스토어에 저장
        - 입력 자료: 데이터 정의서, 데이터 획득 계획서, 데이터 스토어 설계서
        - 처리 및 도구: 데이터 추출(크롤링) 도구, 데이터 수집 스크립트, ETL(Exract, Transform, Load) 도구
        - 출력 자료: 수집된 데이터
    - Step 3.2 데이터 정합성 검토 (Data Consistency Review): 데이터 품질 점검을 통하여 데이터의 정합성을 확보
        - 입력 자료: 수집된 데이터, 데이터 정합성 규칙
        - 처리 및 도구: 데이터 정합성 검사 도구, 데이터 품질 검사
        - 출력 자료: 데이터 정합성 검토 결과 보고서<br>
<br>

* **Task 4 분석용 데이터셋 생성 및 데이터 품질 관리 (Analysis Dataset Creation & Data Quality Management)**
    * Step 4.1 분석용 데이터셋 생성 (Analysis Dataset Creation)
        * 입력 자료: 수집된 데이터, 데이터 변환 규칙
        * 처리 및 도구: 데이터 전처리 도구, 데이터 변환 프로세스
        * 출력 자료: 분석용 데이터셋
    * Step 4.2 데이터 품질 관리 (Data Quality Management)
        * 입력 자료: 분석용 데이터셋, 데이터 품질 기준
        * 처리 및 도구: 데이터 품질 관리 도구, 데이터 품질 모니터링
        * 출력 자료: 데이터 품질 관리 보고서

#### Phase 3 데이터 분석 (Data Analysis)

- **Task 1 분석용 데이터 준비(Analysis Data Preparation)**
    - Step 1.1: 정형 데이터 준비 (Structured Data Preparation)
        - 입력 자료: 정형 데이터셋, 데이터 정의서, 데이터 스토어
        - 처리 및 도구: 데이터 선정, 분할, 샘플링, 필터링, 통합, 변환
        - 출력 자료: 분석용 정형 데이터셋
    - Step 1.2: 비정형 데이터 준비 (Unstructured Data Preparation)
        - 입력 자료: 비정형 데이터셋, 텍스트/이미지/비디오 데이터, 데이터 정의서, 데이터 스토어
        - 처리 및 도구: 토큰화, 불용어 제거, 형태소 분석, 어간/키워드 추출, 텍스트 정규화, 이미지/비디오 전처리(크기 조정, 노이즈 제거, 특징 추출)
        - 출력 자료: 분석용 비정형 데이터셋<br>
<br>

- **Task 2 탐색적 분석 (Exploratory Analysis)**
    - Step 2.1 탐색적 데이터 분석 (EDA): 다양한 관점에서 데이터의 분포 및 특성 확인
        - 입력 자료: 분석용 데이터셋
        - 처리 및 도구: EDA 도구, 통계 분석 (기술통계·추론통계), 변수 간 연관성 분석 (상관 분석, 교차 분석), 데이터 분포 확인 (히스토그램, 박스 플롯), 이상치 탐지
        - 출력 자료: 데이터 탐색 보고서
    - Step 2.2 탐색적 데이터 시각화 (Data visulisation): 데이터 시각화는 탐색적 데이터 분석을 위해 활용
        - 입력 자료: 분석용 데이터셋, 시각화 도구
        - 처리 및 도구: 데이터 시각화 (막대 그래프, 선 그래프, 산점도), 인포그래픽, 통계 시각화
        - 출력 자료: 데이터 시각화 보고서<br>
<br>

- **Task 3 모델링 (Modeling)**
    - Step 3.1 데이터 분할 (Data Partitioning): 모델의 과적합 문제 해결과 모델의 검증력을 테스트하기 위한 데이터 분할 
        - 입력자료: 분석용 데이터셋
        - 처리 및 도구: 데이터 분할 패키지
        - 출력자료: 훈련용 데이터셋, 테스트용 데이터셋
    - Step 3.2 정형 데이터 모델링 (Structured Data Modeling)
        - 입력자료: 분석용 데이터셋, 데이터 마이닝 도구.
        - 처리 및 도구: 
            1. 분류: 의사 결정 트리, 로지스틱 회귀 
            2. 회귀: 선형 회귀, 다항 회귀
            3. 군집화: K-평균, 계층적 군집화
            4. 연관 규칙 학습: Apriori, FP-Growth
        - 출력자료: 정형 데이터 마이닝 모델
    - Step 3.3 텍스트 데이터 모델링 (Text Data Modeling)
        - 입력자료: 분석용 텍스트 데이터, 텍스트 마이닝 도구
        - 처리 및 도구: 텍스트 분류, 감성 분석, 토픽 모델링, 텍스트 요약, 개체명 인식
        - 출력자료: 텍스트 분석 결과 보고서
    - step 3.4 모델 적용 및 운영 방안 (Model Deployment & Monitoring): 모델 적용을 위한 상세한 알고리즘 설명 작성과 모델의 운영 모니터링 방안 수립 
        - 입력자료: 모델링 결과 보고서
        - 프로세스 및 도구: 모니터링 방안 수립, 알고리즘 설명서 작성
        - 출력자료: 모델 운영 방안 보고서<br>
<br>

- **Task 4 모델링 및 평가/검증 (Modeling & Evaluation/Validation)**
    - Step 4.1: 모델링 (Modeling)
        - 입력자료: 분석용 데이터셋, 모델링 도구
        - 처리 및 도구: 모델링 알고리즘 선택, 모델 학습 및 튜닝
        - 출력자료: 모델링 결과
    - Step 4.2: 모델 평가/검증 (Evaluation/Validation)
        - 입력자료: 모델링 결과, 검증 데이터셋
        - 처리 및 도구: 모델 성능 평가 지표, 교차 검증
        - 출력자료: 모델 평가/검증 보고서

#### Phase 4 시스템 구현 (System Implementation)

* **태스크 1: 분석 모델 기반 시스템 설계 및 구현 (Analysis Model-based System Design & Implementation)**
    * 스텝 1.1: 분석 모델 기반 시스템 설계 (Analysis Model-based System Design)
        * 입력자료: 모델링 결과, 시스템 요구사항.
        * 처리 및 도구: 시스템 아키텍처 설계, API 설계.
        * 출력자료: 시스템 설계서
    * 스텝 1.2: 시스템 구현 (System Implementation)
        * 입력자료: 시스템 설계서, 개발 도구.
        * 처리 및 도구: 시스템 개발, 코드 리뷰.
        * 출력자료: 구현된 시스템
* **태스크 2: 시스템 테스트 및 운영 환경 구축 (System Test & Operation Environment Setup)**
    * 스텝 2.1: 시스템 테스트 (System Test)
        * 입력자료: 구현된 시스템, 테스트 케이스.
        * 처리 및 도구: 단위 테스트, 통합 테스트, 성능 테스트.
        * 출력자료: 시스템 테스트 결과 보고서
    * 스텝 2.2: 운영 환경 구축 (Operation Environment Setup)
        * 입력자료: 구현된 시스템, 운영 환경 요구사항.
        * 처리 및 도구: 서버 구축, 배포 자동화.
        * 출력자료: 구축된 운영 환경

**5. 평가 및 전개 (Evaluation & Deployment)**

* **태스크 1: 분석 결과 평가 및 모델 발전 계획 수립 (Analysis Result Evaluation & Model Development Plan)**
    * 스텝 1.1: 분석 결과 평가 (Analysis Result Evaluation)
        * 입력자료: 모델 평가/검증 보고서, 비즈니스 목표.
        * 처리 및 도구: 비즈니스 영향 분석, 모델 성능 평가.
        * 출력자료: 분석 결과 평가 보고서
    * 스텝 1.2: 모델 발전 계획 수립 (Model Development Plan)
        * 입력자료: 분석 결과 평가 보고서, 모델 개선 아이디어.
        * 처리 및 도구: 모델 개선 방향 설정, 모델 재학습 계획.
        * 출력자료: 모델 발전 계획서
* **태스크 2: 프로젝트 성과 보고 및 시스템 전개 (Project Performance Report & System Deployment)**
    * 스텝 2.1: 프로젝트 성과 보고 (Project Performance Report)
        * 입력자료: 분석 결과 평가 보고서, 프로젝트 결과.
        * 처리 및 도구: 프로젝트 성과 요약, 보고서 작성.
        * 출력자료: 프로젝트 성과 보고서
    * 스텝 2.2: 시스템 전개 (System Deployment)
        * 입력자료: 구현된 시스템, 운영 계획.
        * 처리 및 도구: 시스템 배포, 사용자 교육.
        * 출력자료: 전개된 시스템

이러한 단계, 태스크, 스텝별 상세화는 프로젝트의 체계적인 관리를 가능하게 하며, 각 단계별 산출물을 명확히 정의하여 품질 관리를 용이하게 합니다.

