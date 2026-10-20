# 공기질(Air Quality UCI) 시계열 예측: 1D-CNN · LSTM · GRU 비교

벤젠 농도(`C6H6(GT)`)를 예측하는 분석입니다. 상관관계를 기준으로 입력 변수를 두 그룹으로 나누고, 그룹마다 **1D-CNN, LSTM, GRU**의 예측 성능을 비교했습니다.

## 데이터셋

- 파일: `project_air/AirQualityUCI.csv` (UCI Air Quality, 구분자 `;`, 소수점 `,`)
- 이탈리아 도시의 대기질 센서 데이터를 1시간 단위로 기록한 것입니다(CO, NMHC, 벤젠, NOx, NO2, O3 센서값, 온도·습도 등).

## 소스 구성

```text
project_air/
└── project_air/
    ├── AirQualityUCI.csv
    └── AirQualityUCI_Model_Process.ipynb  # 전처리 → 시각화 → 모델 학습·비교
```

## 분석 내용

1. **전처리**: 빈 열과 결측 행을 제거하고, 날짜와 시간을 합쳐 시간 인덱스를 만들고, 결측치 표시값인 `-200`을 제거합니다.
2. **시각화**: 주요 오염물질(벤젠, CO, NOx)의 시간별 추이와 변수 간 상관관계 히트맵을 그립니다.
3. **변수 그룹 분리**
   - 고상관 그룹: `C6H6(GT)`, `PT08.S2(NMHC)`, `PT08.S5(O3)`
   - 저상관 그룹: `T`, `RH`, `AH` + 타깃
4. **시퀀스 생성**: 24시간 길이 윈도우를 만들고 MinMax 정규화를 적용합니다.
5. **모델 비교**: 그룹마다 1D-CNN, LSTM, GRU를 학습하고, 예측 그래프와 MSE를 비교합니다.

## 결과

결과는 노트북의 그래프로 확인할 수 있습니다.
- 그룹별·모델별 실제값과 예측값 비교 그래프
- 그룹별 세 모델의 MSE 비교 그래프

## 실행 방법

```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow
cd project_air
jupyter notebook AirQualityUCI_Model_Process.ipynb
```
