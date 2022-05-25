# KIST_predict_plant_weight
생육 환경 최적화 경진대회

## 개발 환경
- OS: Windows 10
- CPU: i9-10900K
- GPU: RTX3070
- Memory: 32GB

## 라이브러리 버전
- torch == 1.7.1+cu110
- torchvision == 0.8.2+cu110
- timm == 0.5.4
- albumentations == 1.1.0
- numpy==1.19.5   
- pandas==1.3.2
- opencv-python==4.2.0  


## 주요 전략
- 하루 뒤의 무게 예측값이 불안정한 것으로 판단하여, 청경채 사진의 현재 무게를 예측한 모델(resnet50, seresnet50)과 하루 뒤의 무게를 예측한 모델(resnet50)을 앙상블하여 최종 제출했습니다.
- 메타 데이터는 검증셋에서는 효과가 있었으나, 테스트셋에서 과적합되는 경향이 있어서 사용하지 않았습니다.

## 전처리
- CASE45-17번은 사람 손이 노출되어 훈련 데이터에서 제외하였습니다.
- 타겟 값은 로그 변환하였습니다.
- CASE73번을 제외하고, 각 CASE는 연속적인 생육 과정으로 가정하고 현재 무게에 대한 레이블을 새로 만들었습니다. 
    - CASE73은 0-9, 10-13, 14-34를 각각의 생육 과정으로 가정하였습니다.

## 실행 방법
### 데이터 경로
- 데이터 경로: 대회에서 받은 train, test 폴더 (./train, ./test)
- 모델 경로: ./saved
- 제출 파일 경로: ./submission

### 노트북 실행 순서
- 아래 순서대로 노트북 실행
1. 학습 및 테스트용 데이터셋 생성: make_dataset.ipynb
    - 5개의 피클 파일 생성됨
2. 각 모델 및 제출 파일 생성: res50_train_future_weight.ipynb, res50_train_current_weight.ipynb, seres50_train_current_weight.ipynb
3. 3개 모델의 제출 파일 앙상블: ensemble.ipynb
