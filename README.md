# ⚡ WhyNot 7기 소프트웨어 캠프 - PySpark 실습 포트폴리오

이 저장소는 WhyNot 7기 소프트웨어 캠프에서 수행한 PySpark 실습 및 프로젝트 결과물을 정리한 포트폴리오입니다.  
RDD부터 DataFrame, SQL, 머신러닝까지 분산 데이터 처리의 흐름을 실습 위주로 학습했습니다.

---

## 📂 PySpark 실습 파일 정리

| 번호 | 파일명                           | 주제 요약                             |
|------|----------------------------------|----------------------------------------|
| 00   | `00_hello_pyspark.ipynb`         | PySpark 환경 설정 및 Hello World 테스트 |
| 01   | `01_start_spark.ipynb`           | SparkSession 생성 및 기본 구조 이해      |
| 02   | `02_RDD_test.ipynb`              | RDD 기초 실습 (생성, map, reduce 등)     |
| 02-1 | `02_mnm_result_load.py`          | MNM 데이터 불러오기 및 RDD 활용 실습     |
| 03   | `03_KVRDD.ipynb`                 | (key, value) 구조 기반 RDD 연산 실습     |
| 04   | `04_Operations.ipynb`            | Transformation & Action 종합 실습       |
| 05   | `05_SparkSQL_DF.ipynb`           | DataFrame과 SQL 활용                    |
| 06   | `06_SparkDataAnal.ipynb`         | DataFrame 기반 EDA 및 정제              |
| 07   | `07_Classification.ipynb`        | 분류 모델 (Logistic Regression 등) 실습 |
| 08-1 | `08_01_Regression_1.ipynb`       | 회귀모델 (단순선형회귀) 실습            |
| 08-2 | `08_02_Regression.ipynb`         | 회귀모델 (다중회귀, 성능 평가 등) 실습  |
> 각 실습은 주제별로 정리되어 있으며, 코드와 결과를 확인할 수 있습니다.

---

## 🛠 사용 기술 스택

- **PySpark 3.5+**
  ![Spark](https://img.shields.io/badge/PySpark-EE7C15?logo=apachespark&logoColor=white)
- **Python 3.12** ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
- **Jupyter Notebook** ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)
- **Docker** ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
- **XShell** ![Xshell](https://img.shields.io/badge/Xshell-DC1F29?logo=gnu-bash&logoColor=white)
- **VMware**  ![VMware](https://img.shields.io/badge/VMware-607078?logo=vmware&logoColor=white)
- **Ubuntu 22.04** ![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?logo=ubuntu&logoColor=white)

---

## 🚀 예시 프로젝트: NYC FHV 승하차 분석

**설명:**  
`fhvhv_tripdata_2020-03.csv`와 `taxi_zone_lookup.csv`를 활용해 NYC 내 FHV 서비스의 승하차 분포를 분석하였습니다.

### 📌 주요 분석
- 서비스존별 승차/하차 건수 집계
- `Manhattan` 지역의 주요 하차 지점 필터링
- PySpark SQL ↔ DataFrame API 변환 실습

### 🔍 주요 코드 예시

```python
pickup_df = trip_df.join(zone_df, trip_df.PULocationID == zone_df.LocationID) \
    .groupBy("Zone").agg(count("*").alias("pickup_count"))

dropoff_df = trip_df.join(zone_df, trip_df.DOLocationID == zone_df.LocationID) \
    .groupBy("Zone").agg(count("*").alias("dropoff_count"))

summary_df = pickup_df.join(dropoff_df, "Zone", "outer").na.fill(0)


