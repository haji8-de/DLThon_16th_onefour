# DLThon_16th_onefour
아이펠 ai 리서처 16th 과정 DLThon 입니다.  


# 🛡️ Data-Centric AI: 대화형 위협/협박 데이터 탐지 성능 향상

> **DLThon 16th Team OneFour (4조)** > **주제:** 학습 데이터 분석 및 증강/정제를 통한 모델 일반화 성능 향상

## 📌 Project Overview
본 프로젝트는 모델의 구조를 변경하지 않고, **데이터의 질(Quality)과 양(Quantity)을 개선**하여 대화형 텍스트 내의 위협(Threat) 및 갈취(Extortion) 상황을 탐지하는 모델의 성능을 극대화하는 것을 목표로 합니다.

단순한 데이터 증강을 넘어, **LLM을 활용한 정교한 합성**, **Hard Negative 마이닝**, **AI 판사(AI Judge) 기반의 노이즈 필터링** 등 고도화된 데이터 처리 파이프라인을 구축하였습니다.

## 👥 Team Members
| 하지양 | 정현석 | 채세현 | 정재훈 | 
| :---: | :---: | :---: | :---: |  
| @haji8-de | @jhs3549 | @sshqwer28 | wogns3764 | 
| 팀장/라벨러 | 모델구현 | 모델구현 | 데이터준비 | 

## 🏗️ Pipeline Architecture

전체 파이프라인은 **데이터 분석(EDA) → 데이터 증강(Augmentation) → 데이터 정제(Cleaning) → 학습 및 평가(Train/Eval)** 단계로 구성됩니다.

### 1. 🔍 EDA (Exploratory Data Analysis)
데이터의 불균형과 잠재적인 문제를 파악하기 위해 심층적인 분석을 수행했습니다.
- **Embedding Clustering:** 임베딩 벡터 시각화를 통해 데이터 분포 확인 및 이상치 탐지
- **Similarity Analysis:** 클래스 간 유사도 분석을 통해 모호한 경계(Decision Boundary) 식별
- **Keyword Extraction:** 협박/갈취 클래스에 주로 등장하는 핵심 키워드 및 토큰 분석

### 2. 🧬 Data Augmentation (LLM-based)
데이터 부족 문제와 클래스 불균형을 해결하기 위해 LLM을 적극 활용했습니다.
- **Contextual Synthesis:** 단순 유의어 교체가 아닌, 문맥을 고려한 고품질 대화 데이터 생성
- **Hard Negative Generation:** 모델이 헷갈려하는 '위협 같지만 위협이 아닌(Normal)' 데이터를 집중적으로 생성하여 오탐(False Positive) 감소 유도
- **Role-Playing Prompt:** 다양한 페르소나를 부여하여 구체적인 협박/갈취 시나리오 생성

### 3. 🧹 Data Cleaning & Filtering
생성된 데이터와 원본 데이터의 신뢰도를 높이기 위한 정제 작업을 수행했습니다.
- **AI Judge:** 생성된 데이터의 레이블 적합성을 판단하는 별도의 LLM 검증 모듈 도입
- **Noise Removal:** 임계값(Threshold) 기반으로 신뢰도가 낮은 데이터 제거
- **Deduplication:** 의미론적 중복 데이터 제거를 통해 과적합 방지

### 4. 🔀 Data Split Strategy
모델의 일반화 성능을 정확히 평가하기 위해 전략적인 데이터 분할을 수행했습니다.
- **Stratified Split:** 클래스 비율을 유지하며 분할
- **Group Split:** 동일 대화/유저의 데이터가 Train/Test에 섞이지 않도록 분리하여 Data Leakage 방지

### 5. 🛡️ Inference Strategy
- **Threshold-based Fallback:** 모델의 예측 확신도(Confidence)가 특정 임계값보다 낮을 경우, 보수적으로 판단하거나 룰 기반 필터링을 거치도록 설계

## 📊 Experiments & Results

| Experiment | Method | F1 Score | 
| :--- | :--- | :---: |
| **Final** | **+ AI Judge Filtering** | **0.780** | 

> *최종적으로 베이스라인 대비 약 00%의 성능 향상을 달성했습니다.*

## 📂 Repository Structure

```

DLThon_16th_onefour/
├── 📁 data/            # (Sample) 데이터셋
├── 📁 img/             # 이미지
├── 📁 models/          # 학습 모델
├── 📁 notebook/        # 노트북 파일
├── 📁 presentiation/   # 발표 자료
└── README.md           # 프로젝트 명세서

```
## 📝 Retrospective (Where We Are)

* **Achievements:** LLM을 활용한 효율적인 데이터 증강 파이프라인 구축, Hard Negative 데이터를 통한 모델의 강건성 확보.
* **Challenges:** 생성된 데이터의 품질을 검증하는 비용(AI Judge)과 시간 문제.
* **Future Works:** 도메인 특화 경량화 모델(sLLM) 도입 고려 및 실시간 필터링 시스템 구축.

