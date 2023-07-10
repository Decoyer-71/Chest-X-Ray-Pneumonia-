# Chest-X-Ray(Pneumonia)

## 주제 
    Chest-X-ray 폐렴(Pneumonia) CNN 분류 모델 생성

## 사용언어
<a href="https://www.python.org/" target="_blank"><img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white"/></a>
<a href="https://jupyter.org/" target="_blank"><img src="https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white"/></a>
<a href="https://www.tensorflow.org/?hl=ko" target="_blank"><img src="https://img.shields.io/badge/Tensorflow-FF6F00?style=flat&logo=tensorflow&logoColor=white"/></a>
<a href="https://keras.io/" target="_blank"><img src="https://img.shields.io/badge/Keras-D00000?style=flat&logo=keras&logoColor=white"/></a>
<a href="https://scikit-learn.org/stable/index.html" target="_blank"><img src="https://img.shields.io/badge/Scikitlearn-F7931E?style=flat&logo=Scikitlearn&logoColor=white"/></a>

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
       
    3) 특징 
        - Train, Test, val폴더로 구성되어 이용이 편리
        - But, validation용도의 Data가 적기에 조정해서 사용할 필요가 있음

## [Image Sample]
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/486f53c9-6c45-4e8e-b907-40d0b596cefe)

## 2. 프로젝트 개요
    1) 목표 
        - Testing 결과 acc 0.90 이상 정확도 모델 생성
        - 계층별, 파라미터별 차이 성능비교
        
    2) 소스명 : data 폴더 -> .ipynb
    
    3) 개발환경 
        - data폴더 -> env_list.txt
        - Google colab(fitting 용)
        
## 3. 비교 실험(Goole colab)
### 1) 계층 비교
#### ※ 공통조건
    - Filter : 64, 128
    - Hidden layer : 2개 (node : 128)
    - Dropout : 0.3
    - Learning rate : 0.0001
    - Padding : same
            
#### (1) C - C - P - C - C - P - F - D - D
        가. Evaluate 결과 : loss: 0.2221 - accuracy: 0.9471
        나. 소요시간 : 0:19:03
        다. 평가 
            - 초반 train 학습이 저조해 보이나 25회 반복을 넘어서면서 역전. 과적합 없음
            - Graph가 고르지 못해 학습률 하향 조정 필요
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/f90f0381-5666-418f-abe1-67fd6cf94ed6)

#### (2) C - P - C - P - C - P - C - P - F - D - D
        가. Evaluate 결과 : loss: 0.2400 - accuracy: 0.9104
        나. 소요시간 : 0:09:24
        다. 평가 
            - (1)번 설정에 비해 학습이 완만하게 이루어지는 경향을 보임. Pooling이 2번 더 추가되면서 이미지 size가 축소하여 계산량이 줄어들었기 때문으로 판단
            - 계산량 차이로 인해 (1)계층에 비해 소요시간이 감소함
            - (1)번 설정과 동일한 pooling 계층을 보유 시 경향 확인이 필요
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/fe54086b-2541-4793-9693-ce819e635cf9)

#### (3) C - P - C - P - C - C - F - D - D
        가. Evaluate 결과 : loss: 0.1457 - accuracy: 0.9522
        나. 소요시간 : 0:11:25
        다. 평가 
            - 과적합 없이 90% 넘는 성능을 보이나, Graph형태로 보아서 학습률 하향 조정 필요
            - (1)번 설정과 동일한 Parameter를 보유하였으나 소요시간이 더 적음, C-P-C 와 C-C-P 계층을 비교해 재검증 필요
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/ba7fabf0-3252-4200-a766-d893869f5f68)

#### (4) C - C - P - F - D - D
        가. Evaluate 결과 : loss: 0.1990 - accuracy: 0.9505
        나. 소요시간 : 0:13:53
        다. 평가 
            - 목표한 성능을 보이나, 과적합이 심함.
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/7a82ba84-6e4f-443d-b936-7d47daf9e5b5)



#### (5) C - P - C - F - D - D
        가. Evaluate 결과 : loss: 0.1797 - accuracy: 0.9608
        나. 소요시간 : 0:09:41
        다. 평가 
            - (4)번 설정 시 소요시간이 더 많은것으로 보아, 연속적인 Conv layer의 연산이 더 높은 성능을 요구하는 것으로 판단      
            - 또한 (4)번과 비교 시 상대적인 성능저하를 보여 특징맵을 1번 추출보다 연속 2번 추출하는 것이 학습률에 더 도움이 되는것으로 판단
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/245f18be-f654-494f-ba81-a1c78b6d28c8)



### 2) 학습률 비교
#### ※ 공통조건
    - 계층비교 5번 모델로 학습률 비교
        · Filter : 64, 128
        · Hidden layer : 2개 (node : 128)
        · Dropout : 0.3
        · Padding : same
        · 계층 : C - P - C - F - D - D ()
    
#### (1) Learning rate : 0.001
        가. Evaluate 결과 : loss: 0.4688 - accuracy: 0.9437
        나. 소요시간 : 0:09:25
        다. 평가 
            - validation loss가 오히려 증가하고, 학습률 0.0001일때와 비교하여 과적합이 심하게 발생
            - 오차를 고려할 때, 학습률을 낮추어야함
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/20c800ef-566b-4761-ae4d-b71259852f42)

#### (2) Learning rate : 1e-5
        가. Evaluate 결과 : loss: 0.1216 - accuracy: 0.9548
        나. 소요시간 : 0:09:36
        다. 평가 
            - 준수한 성능(정확도 90%이상)을 보이며, 과적합 문제도 해소
            - Graph 형태가 고르지 못한 문제
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/b69ec4d7-a148-46ce-82a5-335d5b4bb6d7)

#### (3) Learning rate : 1e-6
        가. Evaluate 결과 : loss: 0.1873 - accuracy: 0.9309
        나. 소요시간 : 0:09:36
        다. 평가 
            - 과적합이 없고, (2)번에 비해 학습 Graph 모양이 고르게 안정적이다.
![image](https://github.com/Decoyer-71/Chest-X-Ray-Pneumonia-/assets/127948197/cd41a404-77c5-44b0-9db0-4a132f07c4f7)



## 결론
### 1) 
### 2) 
### 3) 
### 4) 
### 5) 
    



  
