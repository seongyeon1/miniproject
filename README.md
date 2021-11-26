# CSLEE 미니프로젝트(어디차리쥬)
![image](https://user-images.githubusercontent.com/83098550/143568576-850856c5-61c9-49d2-aed4-51a99551f83a.png)
- 양질의 일자리와 경제성장 : 자영업자의 효율적인 요식 업체 진출을 통하여 일자리 창출과 지속성을 이어 나갈 수 있도록 함
- 지속가능한 도시와 공동체 : 도시와 주거지에서의 안정적인 경제 생활 구축을 목표로 함

## 분석배경
코로나19로 인한 외식&배달의 비중 변화
![image](https://user-images.githubusercontent.com/83098550/143569052-0f7ac730-54b0-4006-b284-c87d5bb1cfd2.png)
![image](https://user-images.githubusercontent.com/83098550/143569076-54d30178-3710-4090-b4b1-c0f3e0be295c.png)

1. 정확하고 안정적인 정보 : 개인 창업이 지속적으로 이루어지고 있으며, 그 중에서 비율이 높은 요식업을 차리려는 사람들에게
체계적인 정보를 제공하여 요식업 발전에 이바지 하고 싶다.

2. 코로나19 패러다임의 변화 : 코로나19가 장기화되면 외식&배달의 비중 변화가 요동치기 때문에 
좀 더 요식업계의 정확한 매출 분석이 필요하다.

## 활용 데이터
- 서울 열린데이터 광장의 요식업 매출 통계 전반을 수집하였다
- 파일의 용량과 컴퓨터의 성능상 2020년 1분기~4분기의 자료만을 이용하였다.
- 이번 프로젝트에서는 데이터 전처리, EDA, 머신러닝, 딥러닝을 진행해 다음 년도의 매출을 예측해보았다.

## 데이터 전처리
- 데이터 중 필요한 데이터만 추출&통합
![GOMCAM 20211126_1954330867](https://user-images.githubusercontent.com/83098550/143570073-eb0e41e9-e842-4269-8339-de5b7221d438.png)

### 분기별 요일에 따른 매출
![GOMCAM 20211126_1957000098](https://user-images.githubusercontent.com/83098550/143570398-4fa83b34-a7b9-44c3-b2f1-5213e44d1ec7.png)

- 이 과정을 통해 멀티인덱스 기능을 배울 수 있었다.

## 데이터 분석
### 분기가 거듭될수록 금요일 매출액이 줄어들고 있다
  -> 코로나로 인해 주중의 외식 패턴이 변화함
  -> 직장인들의 회식 문화가 축소됨에 따른 것이라 추정된다 

![image](https://user-images.githubusercontent.com/83098550/143570735-ae1f250a-8018-4977-ac2e-044e327f0c94.png)

### 주중매출은 직장인구수의 영향을 많이 받는다
- 서울지역의 자료만을 사용했기에 서울지역특성상 매출금액이 개업점포수나 직장인구의 영향을 많이 받는 것일 가능성이 크다
- 코로나에 따른 유동인구의 영향력이 감소했을 가능성도 있다
![image](https://user-images.githubusercontent.com/83098550/143571055-f09ceef5-9610-479b-9d24-7e0f6571bc65.png)

### 주말매출은 직장인구보다는 점포수의 영향을 많이 받는다
![image](https://user-images.githubusercontent.com/83098550/143571199-6014e528-8de7-4380-a00e-626ce6a6a047.png)

### 주중과 주말에 따라 매출에 영향을 미치는 요인의 양성이 달라짐을 알 수 있다
![image](https://user-images.githubusercontent.com/83098550/143571365-a94182f1-da4d-490a-8223-bff246a1abc7.png)

### 매출자료들을 찾아본 결과 다양한 구분으로 매출자료들이 나눠져 있었다
- 이걸 그냥 단순 분기별 총 매출만 예측하기엔 아깝다는 생각이 들었다
- 요일에 따른 매출을 예측하고 합하는 식으로 계산하는 것이 더 좋을 것 
   같다는 생각으로 매출 예측 방향을 생각해 냄


## 머신러닝 (1)
### 주중과 주말에 미치는 영향이 다르니 히트맵에서 상관관계가 높은 20개 추출
![image](https://user-images.githubusercontent.com/83098550/143571697-0ed114ca-2100-4385-9487-7347a5e17780.png)
![image](https://user-images.githubusercontent.com/83098550/143571705-d648c926-85b0-4e2a-9bd5-24364c6674c8.png)

월요일 매출에 영향을 주는 컬럼들로 월요일 매출을 예측
![GOMCAM 20211126_2021510412](https://user-images.githubusercontent.com/83098550/143573734-b3f382e8-b340-4866-97e4-4f7f8fcd08b0.png)

로그를 취해 매출의 분포가 정규분포에 가깝게 하여 정확도를 높이고자 하였다
![GOMCAM 20211126_2009020346](https://user-images.githubusercontent.com/83098550/143571972-6db5d909-7325-44a5-905a-dfcf72f4a8e5.png)

![image](https://user-images.githubusercontent.com/83098550/143573989-d6bc8098-0148-4ea4-aeb2-a490152fda8d.png)
![image](https://user-images.githubusercontent.com/83098550/143574009-0bc36d08-a1da-4d86-9004-21c2042a7a7d.png)
다양한 모델을 돌려본 결과 Random Forest 모델이 가장 성능이 좋았다

Y값을 여러 가지를 한번에 예측할 수 있을까?

## 머신러닝 (2)
- 전체를 한 번에 예측 가능하다
![image](https://user-images.githubusercontent.com/83098550/143577010-e0fea6b6-cf5e-4738-90f5-d0472c8b2eba.png)

### Y가 복수의 변수일 경우에도 이 함수가 적용 될 수 있다.
![image](https://user-images.githubusercontent.com/83098550/143577182-4049023d-3884-477d-adc1-39b48b0a3895.png)

![image](https://user-images.githubusercontent.com/83098550/143577280-3ba90d7c-f280-47dd-adec-7f3b2276677e.png)

![image](https://user-images.githubusercontent.com/83098550/143577411-27060b81-5650-4a2c-873c-5b7d0114d1d9.png)




## 활용방안

## 
