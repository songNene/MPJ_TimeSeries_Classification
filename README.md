# 🕒 Time Series Classification Mini Project

## 📌 프로젝트 목표
- 비정상 시계열 데이터를 정상 시계열로 변환해보기
- 다양한 분류 모델(Logistic Regression, Random Forest, XGBoost, Gradient Boosting)을 활용하여 고장 여부(classification)를 정확히 예측
- tsfresh 라이브러리를 활용해 유의미한 시계열 특징(feature)을 추출하고 모델 성능 향상 도모

---

## 🧪 데이터 및 전처리 과정
본 프로젝트에서는 `AirPassengers` 데이터를 기반으로 다음과 같은 과정을 수행했습니다:

1. **로그 변환 (Log Transformation)**  
   - 분산을 일정하게 만들고 왜도(Skewness), 첨도(Kurtosis)를 줄이기 위해 log 변환을 수행했습니다.

2. **차분(Differencing)**  
   - 데이터의 추세(Trend)를 제거하고 정상성을 확보하기 위해 `.diff()`를 활용한 1차 차분 수행

3. **계절 차분(Seasonal Differencing)**  
   - AirPassengers 데이터의 계절성(12개월 주기)을 제거하기 위해 `.diff(12)` 수행

4. **ADF 테스트를 통한 정상성 검정**  
   - 단위근이 없고 정상성을 갖는 시계열 데이터로 변환되었음을 검정

---

## 🧠 특징 추출 및 분류 모델 적용
`tsfresh`의 `EfficientParameters`를 활용하여 고장 유무를 분류할 수 있는 다양한 시계열 특징을 생성하였습니다. 주요 특징 중 하나였던 `F_X_abs_energy`는 최종 예측 결과에 큰 영향을 미친 핵심 피처였습니다.

이후 다음 모델들을 적용하여 분류 성능을 비교하였습니다:

- **RandomForestClassifier**
- **XGBoostClassifier**
- **LogisticRegression**
- **GradientBoostingClassifier**

---

## 📈 모델 성능 비교

### 🎯 Logistic Regression
- Accuracy: 57.14%
- Ture class precision: 1.0, recall: 0.44
- False class precision: 0.36, recall: 1.0  
→ 클래스 간 성능 차이가 크고 비대칭적인 예측 패턴

### 🎯 Gradient Boosting
- Accuracy: 95.24%
- Ture class precision: 1.0, recall: 0.94
- False class precision: 0.83, recall: 1.0  
→ 안정적이고 균형 잡힌 분류 성능

### 🎯 XGBoost
- Accuracy: 1.0 (100%)
→ 과적합 가능성 의심. 높은 정확도이지만 feature leakage 또는 단순한 분류 경계일 수 있음

---

## 📚 분류 리포트 해석
`classification_report`를 통해 precision, recall, f1-score, support 등 각 클래스별 모델 성능을 수치로 평가하였으며, macro avg와 weighted avg를 통해 전체 모델의 균형 성능을 검토하였습니다.

---

## 🔧 사용 라이브러리
- Python 3.x
- pandas, numpy, matplotlib
- scikit-learn
- tsfresh
- xgboost
