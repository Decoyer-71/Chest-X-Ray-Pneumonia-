# Chest-X-Ray(Pneumonia)

## 주제 
    Chest-X-ray 폐렴(Pneumonia) CNN 예측 모델 생성

## 사용언어
<a href="https://www.python.org/" target="_blank"><img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white"/></a>
<a href="https://jupyter.org/" target="_blank"><img src="https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white"/></a>

## 폴더 분류
[code](https://github.com/Decoyer-71/BrainTumor/tree/master/code) : 학습 및 모델생성 코드


## 1. Data Set
    1) 출처 : [Kaggle Chest X-Ray Images (Pneumonia)](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia)
    2) 구성
        - Test 폴더 
          · NORMAL 폴더 : 234개
          · PNEUMONIA 폴더 : 390개
        - Train 폴더 
          · NORMAL 폴더 : 1341개
          · PNEUMONIA 폴더 : 3875개
        - val 폴더 
          · NORMAL 폴더 : 8개
          · PNEUMONIA 폴더 : 8개
        - Label : NORMAL, PNEUMONIA

## 2. 프로젝트 개요
    1) 목표 
        - Testing 결과 acc 0.90 이상 정확도 모델 생성
        - 계층별, 파라미터별 차이 성능비교
    2) 소스명 : data 폴더 -> .ipynb
    3) 개발환경 
        - data폴더 -> env_list.txt
        - Google colab(fitting 용)
        
## 계층별 / 파라미터별 실험(Goole colab)
### 1) 계층 비교
### ※ 공통조건
    - Filter : 64, 128
    - Hidden layer : 2개 (node : 128)
    - Dropout : 0.3
    - Learning rate : 0.0001
            
        (1) C - C - P - C - C - P - F - D - D
            가. Evaluate 결과 : loss: 0.2221 - accuracy: 0.9471
            나. 소요시간 : 0:19:03
            다. 평가 
                - 초반 train 학습이 저조해 보이나 25회 반복을 넘어서면서 역전. 과적합 없음
                - graph가 고르지 못해 학습률 하향 조정 필요
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/f90f0381-5666-418f-abe1-67fd6cf94ed6)




## 결론
### 1) 
### 2) 
### 3) 
### 4) 
### 5) 
    



  
