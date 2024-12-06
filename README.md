# 유전자 발현 정도 활용 유방암 예측

<br>

## 진행기간
> **2022/09~12**
<br>


## 사용 데이터
> **National Cancer Institute(국립암연구소)에서 진행되는 프로젝트 중 하나인 TCGA(The Cancer Genome Atlas) 에서 기탁된 유방암 조직 샘플데이터**
<br>

## 개발 환경
> **Python**
<br>

### 역할
> **EDA,  Data Preprocessing, Modeling, ppt 작성**
<br>

## 분석 주제
> **mRNA 발현 정도를 활용한 유방암 예측**
<br>


## 분석 요약

1. EDA
2. Data Preprocessing
    1. 변수 선택(Levene’s test, Shapiro Wilks test, Student t-test, Wilcoxon rank sum test)
    2. PCA, ICA
3. Modeling
    1. 예측 모델(LR, RF, XGB)
    2. 군집 모델(Kmeans)
4. 모델 해석
<br>

## 분석 과정

### *EDA&Data Preprocessing*
<br>

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/49ea475a-b09b-4873-8aa3-65b7badf4504" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/95809509-ecfb-40a9-a8cc-8af51dea2a40" width="95%">
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/cabf6bb4-96ec-441c-b6ab-f8b46bc7a370" width="48%">
    </td>
  </tr>
</table>
<br>

- 굉장히 많은 열을 가져서 열을 줄이는 방법 필요

<br>

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/3d8cbfaa-1f23-43ef-bf89-9803b4687287" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/8386399b-b4c1-4b7e-b611-689eefd9c488" width="95%">
    </td>
  </tr>
</table>
<br>

- `평균 비교 검정`을 진행하여 유의한 변수를 선택(target은 유방암 발생 여부)
    - 검정을 진행하기 전 `등분산성`을 확인

<br>

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/913d6a6a-980f-44ba-9237-c9f4dbcd3465" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/8b09e83f-de91-47e8-a753-dacba8c7dfcb" width="95%">
    </td>
  </tr>
</table>
<br>

- PCA, ICA 차원 축소 기법을 활용하여 최대한 적은 변수를 선택할 수 있도록 함
- `PCA`는 정규성을 따르며 평균차이가 유의한 변수들로 추출
- `ICA`는 정규성을 따르지 않으나 평균차이는 유의했던 변수들로 추출

<br>

### *Modeling: 예측 모델*
<br>
<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/4853336a-96fe-4020-99a9-735bbb4a3cdc" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/6cb59f11-ea53-4151-bc29-1a7f7592b0db" width="95%">
    </td>
  </tr>
</table>
<br>

- Logistic Regression의 경우 변수의 정규분포 가정이 필요하므로 ICA를 통해 구한 변수는 제외하여 비교
- 정규성을 만족하는 변수나 주성분만을 사용했을 때 성능도 향상되고 시간 단축도 크게 이루어짐
    - 정규성과 다중공선성 문제가 해결되 나타난 결과로 보임

<br>

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/33174549-8577-4861-a97e-95ded1e6d983" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/1c11765f-fc6c-4d3c-8dca-2a47e08a5480" width="95%">
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/1530b990-0c92-44ba-ad46-6426ab32317a" width="60%">
    </td>
  </tr>
</table>
<br>

- Random Forest의 경우 성능 차이는 두드러지지는 않지만 시간단축은 유의미 했음

<br>

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/c0a2eaad-6043-4501-b162-a4e5d5e9feef" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/0f3086d0-dc05-4b2a-9f06-c16d4f8e7e10" width="95%">
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ea91bc6c-3884-4d9b-a74f-b5f76aa3d70d" width="60%">
    </td>
  </tr>
</table>
<br>

- XGBoost도 성능에 차이는 없으나 시간 단축이 크게 일어남

<br>

### *Modeling: 군집 모델*
<br>

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/761471e5-019a-4be4-8726-6ad56c6bad33" width="80%">
    </td>
  </tr>
</table>
<br>

- 주성분과 독립성분을 추출할 때 여러 가지 조합으로 시도했으며, 오른쪽 그림과 같이 암 진단 여부가 두드러지게 분리된 최적의 개수로 설정

<br>

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/14b60df5-0848-461b-a6e1-cf7345ffc2d2" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/0ddd92f0-210a-4730-a9c2-8c86818c5b40" width="95%">
    </td>
  </tr>
</table>

<br>

- Elbow plot을 보면 3부터 쭉 k를 어디에 지정해도 무방한 것으로 보임
- k를 지정하기 위해 어떠한 한 집단에 암에 걸린 사람이 최대한 나눠지도록 설정. 이에 적절한 `k는 5`로 지정

<br>

<table width="100%">
  <tr>
    <td align="left" width="70%">
      <img src="https://github.com/user-attachments/assets/6a9413e1-a49c-4036-9c35-45341f36e8db" width="95%">
    </td>
    <td align="right" width="30%">
      <img src="https://github.com/user-attachments/assets/f109fa9d-70ae-4f90-a626-e250fed77026" width="95%">
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/4f25c472-b1f7-4d6f-ab02-ac58b38276f8" width="70%">
    </td>
  </tr>
</table>
<br>

- `4번 집단`에 암에 걸린 사람이 대부분 몰린 것으로 확인
- pair plot에서 `보라색 집단이 4번 집단`으로 PCA1과 ICA3에 의해 다른 집단과 `명확하게 분리`되는 것을 확인할 수 있음
- 주성분에 대한 각 변수의 `기여도`를 살펴본 결과 확실히 `암과 관련된 유전자`가 `발현 정도가 높다는 것`을 알 수 있음

<br>

## 시사점 및 보완할 점

- **예측 모델**
    - 원 변수를 그대로 사용해도 성능이 매우 좋아서 `모델 학습 속도`에 유의하여 프로젝트 진행
    - 약 18000개 가량의 열을 가지고 있어 시간 단축을 위해 다양한 방법 적용
        - `t-test`, `Wilcoxon rank sum test` 등과 같은 `평균 비교 검정`으로 변수 선택
        - `PCA`, `ICA`를 통한 차원 축소 방법 활용
    - Logistic 모형의 경우 PCA를 활용했을 때 극대화된 성능향상과 시간 단축이 이루어 짐
- **군집 모델**
    - `Kmeans`를 통해 암에 걸린 사람들의 집단을 도출해낼 수 있었음
    - Clustering 에서 각 성분들에 대한 해석을 도메인을 가지고 더 진행한다면 다채로운 결과 해석이 가능할 것. 또한 집단 별로 더 자세한 해석을 진행한다면 암에 걸릴 가능성이 있는 집단도 찾을 수 있을 것.
- `Shapiro test`의 경우 매우 엄격하기에 정규성을 가정할 수 있는 변수들을 잃어버렸을 가능성이 존재. 또한 매우 많은 변수를 검정했기 때문에 `1종 오류의 증가`를 감안
    - `다중 비교법`을 활용 한다면 더 좋은 결과를 도출 할 수 있을 것

