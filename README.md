# 서울 다세대/연립주택 전세 가격 예측 서비스 : 성동구 중심으로 

---

### ✏️ 프로젝트 정보
|제목|내용|
|---|---|
|프로젝트 기간  |2023.11.14 ~ 2023.12.04 |
|팀원 구성 |김성우(조장), 이상민(부조장), 황서진, 권예빈, 정태준|
|구성| 1. 2015 ~ 2022년 전세 데이터 탐색적 분석 <br> 2. 전세가격 예측 모델 생성|
|공간적 범위 | 서울특별시|
|시간적 범위 | 2015 ~ 2022년|
#### ⏰ 프로세스
- 데이터 수집 및 정제 
- 기초 EDA 및 시각화
- EDA 기반 가공
- 모델링(회귀)
- 모델 성능 평가
- 인사이트 도출
  
---
### 🔖 소개
>‘전세’는 내 집 마련이 어려운 현대사회에서 청년들의 금융부담을 완화하고, 주거의 안정성을 강화하며 보금자리를 마련해 주는, 현대인에게 내 집 마련의 발판이 되는 소중한 제도 입니다. 

>현재 서울 부동산 시장에서는 예측할 수 없이 변하는 주택 가격과 서울로의 인구유입의 지속으로 지방 소멸화 현상이 동시에 일어나고 있습니다. 이에 따라, 부동산 시장의 불안정성이 높아지고 있으며 특히 전세시장에서는 수요의 변화가 예측하기 어려운 상황입니다.

>이러한 상황에서 데이터 분석을 통한 주택 시장의 변화 및 전세가격의 패턴 분석은 중요한 의미를 가집니다. 전세와 관련된 주택의 특징과 주변환경을 분석함으로써, 전세가격의 적정선을 예측하는 데 도움이 될 것입니다. 

>이를 통해 주거 안정성을 갖추기 위한 정책 및 제도의 개선에 기여할 수 있을 뿐만 아니라, 부동산 시장의 건전성을 유지하는 데 기여할 것으로 예상됩니다. 따라서 이러한 이유로 전세가격과 주택 시장의 데이터 분석은 청년 및 현대인들의 안정된 주거 환경을 보장하기 위한 중요성을 띈다고 파악되어 프로젝트 주제로 ‘모델링을 통한 전세가격예측’을 선정하게 되었습니다.

---
### 📱 데이터
#### 1. Feature 선정
1. `전세거래 데이터` : 2015 ~ 2022 기간의 서울시 구별 전세 계약 데이터

2. `Infra Feature`: cctv 개수, 지하철 역과의 최소거리, 학교와의 최소거리  

3. `Human-related Features`: 범죄 수, 생활만족도, 학생수(초,중,고), 근로자 수

#### 2. Feature 명세서
| 변수명     | 항목명(영문)          | 항목명(한글)    | 항목설명                    |
|------------|-----------------------|-----------------|-----------------------------|
| total_deposit | Total Deposit       | 전월세 보증금   | 월세를 전세로 변환뒤 총 전세 보증금 |
| build_year    | Build Year          | 건축년도        | 건축년도                    |
| deal_y        | Deal Year           | 년              | 계약년도                    |
| dong          | dong                | 법정동          | 서울시 법정동               |
| deposit       | Deposit             | 보증금액        | 보증금(만원)                |
| deal_m        | Deal month          | 월              | 계약월                      |
| m_rent        | Monthly Rent        | 월세금액        | 월세(만원)                  |
| use_area      | Area for Exclusive  | 전용면적        | 전용면적(m²)                |
| floor         | Floor               | 층              | 아파트 층수                 |
| jibun         | Jibun               | 지번            | 주소지                      |
| crime         | Crime               | 범죄            | 서울시 범죄수               |
| students      | Students            | 학생수          | 서울시 초,중,고 학생수      |
| life_satis    | Life Satisfaction   | 생활만족도      | 생활환경 만족도             |
| workers       | Workers             | 근로자수        | 서울 특별시 근로자수        |
| date          | Year                | 년도            | 2023년 - 계약년도           |
| res_cnt       | resturant           | 음식점 수       | 성동구 음식점 수            |
| school_dis    | school_distance     | 학교거리        | 학교까지와의 거리           |
| cctc_cnt      | cctv                | cctv 수         | 동별 cctv 개수              |

---

### ⌛️ 프로젝트 수행 과정
#### 📈 workflow
![image](https://github.com/hwangseojin223/Jeonse_Price_Prediction_Model/assets/79084966/d6d8671d-ad40-4963-8300-0f1942e3c32f)

#### 👩🏻‍🏫 프로젝트 과정
1. 서울특별시 전세거래 데이터에서 <b>특정 구를 선정</b>하기 위하여 구별 학생 수, 범죄 수, 생활만족도, 근로자 수 데이터를 feature로 선정
2. 지역코드, 법정동, 지번, 층, 건축년도, 년, 월, 보증금액, 월세금액, 전용면적   → 전세가와 관련있다고 판단되는 feature를 원데이터에서 추출
3. 전용면적(m^2) -> 평으로 전환
4. 월세 -> 전세로 전환
5. 동년 연도별 평균보증금 구하기
6. 구와 feature(평당 전세가격, 학생 수, 범죄 수, 생활만족도, 근로자 수)별 상관관계를 구한 결과 상관관계가 가장 높은 구는 <b>성동구</b>
![image](https://github.com/hwangseojin223/Jeonse_Price_Prediction_Model/assets/79084966/73b8a1ef-9207-45da-a617-71718476e0ab)
7. 주거 환경의 특성을 종합적으로 고려하기 위한 피쳐 추가 -> 학교와의 거리, 지하철 역과의 거리, CCTV 개수, 음식점 개수
8. 최종데이터

    | Column        | Non-Null Count      | Dtype    |
    |---------------|---------------------|----------|
    | date          | 12211 non-null      | int64    |
    | build_year    | 12211 non-null      | int64    |
    | dong          | 12211 non-null      | object   |
    | floor         | 12211 non-null      | int64    |
    | use_area      | 12211 non-null      | float64  |
    | res_cnt       | 12211 non-null      | int64    |
    | total_deposit | 12211 non-null      | int64    |
    | cctv_cnt      | 12211 non-null      | int64    |
    | school_dis    | 12211 non-null      | float64  |
    | sub_dis       | 12211 non-null      | float64  |   




9. 이상치 확인 및 제거
10. 로그변환
11. Modeling
- LinearRegression
- Ridge
- Lasso
- DecisionTreeRegressor
- RandomForestRegressor
- XGBRegressor
- LGBMRegressor


10. RMSE
    
    10.1 원본 데이터 RMSE
    |Model|RMSE|
    |---|---|
    |LinearRegression| 7024.544|
    |Ridge|7024.62|
    |Lasso|7024.429|
    |DecisionTreeRegressor|6581.42|
    |RandomForestRegressor|5320.244|
    |XGBRegressor|5742.972|
    |LGBMRegressor|5212.359|

    10.2 로그변환 후 RMSE
    |Model|RMSE|
    |---|---|
    |LinearRegression| 0.353|
    |Ridge|0.353|
    |Lasso|0.404|
    |DecisionTreeRegressor|0.365|
    |RandomForestRegressor|0.274|
    |XGBRegressor|0.271|
    |LGBMRegressor|0.283|

    10.3 이상치제거, 로그변환 후 RMSE
    |Model|RMSE|
    |---|---|
    |LinearRegression| 0.353|
    |Ridge|0.335|
    |Lasso|0.393|
    |DecisionTreeRegressor|0.351|
    |RandomForestRegressor|0.261|
    |XGBRegressor|0.256|
    |LGBMRegressor|0.262|

    10.4 이상치제거, 로그변환, 표준화 후 RMSE
    |Model|RMSE|
    |---|---|
    |LinearRegression| 0.335|
    |Ridge|0.335|
    |Lasso|0.464|
    |DecisionTreeRegressor|0.344|
    |RandomForestRegressor|0.261|
    |XGBRegressor|0.256|
    |LGBMRegressor|0.262|    

11. 하이퍼파라미터 설정
12. Importances
    12.1 선형회귀 모델 : use_area 가 가장 높음
    12.2 비선형회귀 모델 : use_area 가 가장 높음
    
13. 최적의 하이퍼파라미터 적용 결과
![image](https://github.com/hwangseojin223/Jeonse_Price_Prediction_Model/assets/79084966/2a958218-16eb-4849-814b-d94442f89cfd)

=> LGBM 모델이 가장 낮으므로 선택

14. 딥러닝 - LSTM
15. 예측 프로그램 구성

---

### 📌 결론 및 향후 과제
>기존의 상식에서 벗어나지 않는 결과(전세 가격은 위치에 영향을 받는다, 전용 면적이 넓을수록 전세값이 높아진다.)를 도출할 수 있었고 다세대 주택의 전세 가격은 아파트와 같이 기존의 예측 가능한 변수들에 영향을 받는다는 것을 확인할 수 있었다.  
>모델링 결과로는 LGBM 의 성능이 가장 좋게 나왔다. 하지만 딥러닝을 추가적으로 실시하고 파라미터 값과 데이터를 더 추가해 모델링을 진행한다면 다른 결과가 나타날 수 있다.  
> 향후 전세 가격 예측 프로그램 구축을 위해서는 더 많은 데이터와 다양한 범주(아파트, 빌딩, 상가 등등) 들도 포함시켜야 한다.  
> 또한 서울시의 특정구만이 아닌 서울시 전체, 전국의 데이터를 추가해 더 많은 범위의 예측을 실시할 수 있다.  
> 예측의정확도를높이기위해지역별특성,산업별근로자분포와같이사회,복지,경제,치안등 포괄적인 변수들을 추가해야 한다.

---

### 💪🏻 느낀점
> 모델링을 위해 데이터 전처리 과정이 중요하다는 것을 느꼈고 모델링 성능을 높이기 위해 하이퍼파라미터를 조정하는 것이 어려웠다. 이후에 변수들을 추가해서 활용성과 정확도 높은 모델을 만들고 싶다.

    
