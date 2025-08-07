# 🌾 조건별 작물 추천 모델링 (PySpark)

## 📌 프로젝트 개요

이 프로젝트는 주어진 환경 조건(토양의 질소, 인, 칼륨 함량, 온도, 습도, pH, 강수량)을 바탕으로 재배하기에 가장 적합한 작물을 추천하는 머신러닝 모델을 개발합니다. PySpark를 활용하여 대규모 데이터셋에 대한 전처리 및 모델링을 수행하며, 로지스틱 회귀 모델을 사용해 분류 문제를 해결합니다.

---

## 💾 데이터셋

* **데이터 출처**: [Crop Recommendation Dataset (Kaggle)](https://www.kaggle.com/datasets/madhuraatmarambhagat/crop-recommendation-dataset?select=Crop_recommendation.csv)
* **컬럼 정보**:
    * `N`, `P`, `K`: 토양의 질소, 인, 칼륨 함량 (mg/kg)
    * `temperature`: 온도 (°C)
    * `humidity`: 습도 (%)
    * `ph`: 토양의 pH 값
    * `rainfall`: 강수량 (mm)
    * `label`: 추천 작물 이름 (총 22가지)

---

## 🛠️ 기술 스택

* **언어**: Python
* **프레임워크**: PySpark (SparkSession, MLlib)
* **라이브러리**: `pyspark.sql`, `pyspark.ml`, `pandas`, `numpy`, `matplotlib.pyplot`

---

## 🚀 프로젝트 진행 단계

1.  **데이터 탐색 및 전처리**:
    * CSV 파일을 PySpark DataFrame으로 로드.
    * `numpy`와 `pandas`를 활용해 데이터 특성 탐색.
    * 결측값(Null/NaN) 확인 및 처리 (데이터셋에 결측값 없음).
    * `label` 컬럼을 `StringIndexer`를 사용하여 숫자 인덱스로 변환.
    * `VectorAssembler`와 `StandardScaler`를 통해 모든 숫자 특성들을 표준화하고 하나의 특징 벡터로 통합.

2.  **모델링 (로지스틱 회귀)**:
    * 데이터를 훈련 세트(80%)와 테스트 세트(20%)로 분할.
    * `LogisticRegression` 모델을 학습 데이터에 맞춰 훈련.

3.  **성능 평가 및 개선**:
    * **1차 평가**: 이상치를 제거하기 전 모델의 전체 정확도는 약 **98.03%**로 측정.
    * **이상치 처리**: `pH` 컬럼의 이상치 30개를 Z-score(임계값 3.0) 방법을 사용하여 제거.
    * **2차 평가**: 이상치가 제거된 데이터로 모델을 재학습시키고, 정확도를 다시 측정.
    * **최종 결과**: 이상치 제거 후 모델의 전체 정확도는 약 **98.89%**로 향상됨. 특히, 쌀(rice)과 같은 일부 작물의 정확도가 개선됨을 확인.
    * **결과 시각화**: `pandas`와 `matplotlib.pyplot`을 사용하여 이상치 제거 전후의 작물별 정확도를 비교하는 테이블 및 그래프를 생성하여 결과를 정리.

---

## ✅ 결과 요약

| | 이상치 제거 전 정확도 | 이상치 제거 후 정확도 |
|:---|:---:|:---:|
| **전체 정확도**| 98.03% | 98.89% |

이상치 제거는 모델의 예측 성능을 소폭 개선하는 데 기여했습니다.

---

## 📈 작물별 정확도 비교 (pH 이상치 제거 전/후)

| Crop | Accuracy_Before | Accuracy_After |
|---|---|---|
| lentil | 1.000000 | 1.000000 |
| maize | 1.000000 | 1.000000 |
| orange | 1.000000 | 1.000000 |
| grapes | 1.000000 | 1.000000 |
| mango | 1.000000 | 1.000000 |
| muskmelon | 1.000000 | 1.000000 |
| pomegranate | 1.000000 | 1.000000 |
| coconut | 1.000000 | 1.000000 |
| jute | 0.900000 | 0.875000 |
| cotton | 1.000000 | 1.000000 |
| papaya | 0.952381 | 1.000000 |
| rice | 0.904762 | 0.944444 |
| banana | 1.000000 | 1.000000 |
| chickpea | 0.909091 | 1.000000 |
| pigeonpeas | 1.000000 | 1.000000 |
| kidneybeans | 1.000000 | 1.000000 |
| blackgram | 0.958333 | 0.952381 |
| coffee | 1.000000 | 1.000000 |
| mungbean | 1.000000 | 1.000000 |
| watermelon | 1.000000 | 1.000000 |
| apple | 1.000000 | 1.000000 |
| mothbeans | 0.964286 | 1.000000 |

---

## ✍️ 실행 방법

이 프로젝트는 Jupyter Notebook 환경에서 PySpark 세션을 생성하여 실행할 수 있습니다. `09_MiniProject_2.ipynb` 파일이 최종 보고서 역할을 하며, 전체 코드와 주석이 포함되어 있습니다.
