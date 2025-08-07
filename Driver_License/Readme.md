# 🚗 Driver License Test Qualification Prediction (PySpark)

이 프로젝트는 운전면허 시험 데이터를 기반으로, 수험자의 다양한 운전 능력 지표와 인구통계적 특성을 활용하여  
**최종 면허 시험 통과 여부(`Qualified`)를 예측하는 머신러닝 모델**을 구축하는 데 목적이 있습니다.

데이터는 [Kaggle Dataset: Driver's License Test Scores](https://www.kaggle.com/datasets/ferdinandbaidoo/drivers-license-test-scores-data)에서 가져왔습니다.

---

## 📊 데이터 개요

| 컬럼명 | 설명 |
|--------|------|
| `Applicant ID` | 수험자 고유 식별자 |
| `Gender`, `Age Group`, `Race`, `Training`, `Reactions` | 범주형 특성 |
| `Signals`, `Yield`, `Speed Control`, `Night Drive`, `Road Signs`, `Steer Control`, `Mirror Usage`, `Confidence`, `Parking`, `Theory Test` | 수치형 운전 평가 점수 |
| `Qualified` | 운전면허 최종 통과 여부 (Yes/No) → ✅ 타겟 변수 |

---

## ⚙ 사용 기술 스택

- **PySpark 3.5.0+**
  ![Spark](https://img.shields.io/badge/PySpark-EE7C15?logo=apachespark&logoColor=white)
- **Python 3.12**
  ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=ffffff)
- **XShell / VMware / Ubuntu 22.04**
- **Docker 환경 (선택적)**

---

## 🧪 전처리 및 모델링 절차

1. **범주형 처리**  
   - `StringIndexer` → `OneHotEncoder` 조합으로 5개 컬럼 인코딩  
   - 예: Gender, Age Group, Race, Training, Reactions

2. **레이블 처리**  
   - `Qualified` → `Pass`로 변환하여 `StringIndexer` 사용

3. **피처 벡터화**  
   - 수치형 점수들과 인코딩된 범주형 벡터를 `VectorAssembler`로 통합

4. **모델 학습**
   - `LogisticRegression` 사용
   - `CrossValidator` + `ParamGridBuilder`를 활용한 하이퍼파라미터 튜닝

5. **성능 평가**
   - `BinaryClassificationEvaluator`로 AUC 및 Accuracy 측정

---

## 🏁 모델 성능

| 지표 | 값 |
|------|----|
| **ROC AUC** | 0.8769 |
| **Accuracy** | 0.8243 |

→ 모델이 평균 이상으로 수험자의 최종 합격 여부를 잘 예측함

---

## 🌟 주요 인사이트

- `Steer Control`, `Theory Test`, `Mirror Usage` 같은 기술 항목이 모델에 큰 영향을 줌
- `Reactions` 같은 심리적 요소는 영향력이 제한적일 수 있음
- 범주형 변수 중 `Training` 유무는 명확한 기준점으로 작용함

---

## 🛠 향후 개선 아이디어

- 🔁 다른 모델과 비교: `RandomForestClassifier`, `GBTClassifier` 등과 성능 비교
- 📊 중요 피처 시각화: feature importance를 통해 불필요한 피처 제거
- ⚖ 클래스 불균형 처리: 비율 확인 후 필요 시 `SMOTE`, `Weighting` 등 시도
- 🪄 모델 앙상블 전략 구성

---

## ✅ To-Do

- [x] PySpark 데이터 전처리 파이프라인 구성
- [x] 로지스틱 회귀 + 파라미터 튜닝
- [ ] Random Forest 성능 비교
- [ ] 모델 설명력 분석
- [ ] GitHub 블로그 포스트 작성

---

## 📁 파일 구조 예시

```bash
driver-license-prediction/
├── data/
│   └── drivers-license.csv
├── notebooks/
│   └── 01_modeling_pipeline.ipynb
├── scripts/
│   └── pipeline.py
└── README.md
