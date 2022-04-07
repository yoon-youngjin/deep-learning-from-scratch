## ch3 신경망
- [x] 가중치를 설정하는 작업(원하는 결과를 출력하도록 가중치 값을 적절히 정하는 작업)은 여전히 사람이 수동으로 함
- [x] ch2에서 게이트의 진리표를 보면서 인간이 적절한 가중치 값을 설정
- [x] 신경망에서 이러한 문제를 해결
- [x] 가중치 매개변수의 적절한 값을 데이터로부터 지동으로 학습하는 능력이 신경망의 중요한 성질

### 퍼셉트론 복습

![image](https://user-images.githubusercontent.com/83503188/161227750-45783848-f269-4c52-b67f-c6fa14084873.png)

- [x] [그림 3-2]는 x1과 x2라는 두 신호를 입력받아 y를 출력하는 퍼셉트론


![image](https://user-images.githubusercontent.com/83503188/161227958-dc1c33d4-bfb5-43d5-97cb-279447ab2f04.png)
- [x] 여기서 b는 **편향**을 나타내는 매개변수로, 뉴런이 얼마나 쉽게 활성화되느냐를 제어
- [x] w1과 w2는 각 신호의 **가중치**를 나타내는 매개변수로, 각 신호의 영향력을 제어
- [x] 여기에 편향을 명시한 결과

![image](https://user-images.githubusercontent.com/83503188/161227757-a1164673-cbfb-4ead-9461-e1fa467c63cd.png)
- [x] 가중치가 b이고 입력이 1인 뉴런이 추가됨
- [x] 해당 퍼셉트론의 동작: x1, x2, 1이라는 3개의 신호가 뉴런에 입력되어, 각 신호에 가중치를 곱한 후, 다음 뉴런에 전달
- [x] 이 신호들의 값을 더하여, 그 합이 0을 넘으면 1을 출력하고 그렇지 않으면 0을 출력
- [x] 조건 분기의 동작(0을 넘으면 1을 출력, 그렇지 않으면 0을 출력)을 하나의 함수 h(x)라 하자

![image](https://user-images.githubusercontent.com/83503188/161228795-465f68d5-c3b2-44e0-912d-407e14779be2.png)

- [x] h(x)라는 함수, 입력 신호의 총합을 출력 신호로 변환하는 함수를 일반적으로 **활성화 함수(activation function)**라 함

![image](https://user-images.githubusercontent.com/83503188/161227791-9281b50d-173d-4f74-9266-80a28518d7d8.png)

### 활성화 함수
- [x] 활성화 함수는 임계값을 경계로 출력이 바뀌는데, 이런 함수를 **계단 함수**라 함

#### 시그모이드 함수
![image](https://user-images.githubusercontent.com/83503188/161227799-ef5cbdce-fd54-45de-b687-5b9c057f5688.png)

- [x] 0 ~ 1사이의 값을 반환하는 함수
- [x] 신경망에서는 활성화 함수로 시그모이드 함수를 이용하여 신호를 변환하고, 그 변환된 신호를 다음 뉴런에 전달

#### 비선형 함수
- [x] 계단 함수와 시그모이드 둘 다 입력이 작을 때의 출력은 0에 가깝고, 입력이 커지면 1에 가까워지는 구조

<p align="center">
  <img src="https://user-images.githubusercontent.com/83503188/162184272-53a9d0ea-6d68-4e73-9523-9c84bcb376b5.png" width="400px" height="250px"/>
  <img src="https://user-images.githubusercontent.com/83503188/162184323-e449d641-1ccc-4b5c-82df-22d1a8183183.png" width="400px" height="250px"/>
</p>

- 또한, 중요한 공통점으로 둘 모두는 비선형 함수 
  > 출력이 입력의 상수배만큼 변하는 함수를 **선형함수**라고 하고, 선형이 아닌 함수가 비선형 함수

#### ReLU 함수
- 입력이 0을 넘으면 그 입력을 그대로 출력하고, 0 이하이면 0을 출력하는 함수

![image](https://user-images.githubusercontent.com/83503188/161227811-9a2fe38b-b2bb-47eb-bdf9-cb640e4d0d08.png)

![image](https://user-images.githubusercontent.com/83503188/161227823-08df86c2-4390-49ae-8287-c9b9f24711f9.png)


#### 신경망에서의 행렬 곱
![image](https://user-images.githubusercontent.com/83503188/161227839-6e74134d-bb8d-47b6-aafa-b6c5de2ffe18.png)

```
X = np.array([1,2]) //( 1,2)
W = np.array([[1,3,5],[2,4,6]])
Y = np.dot(X, W)
```

#### 항등 함수와 소프트맥스 함수
- 항등 함수: 입력을 그대로 출력 -> 입력과 출력이 항상 같음
- 소프트맥스 함수 
  - 입력을 0 ~ 1사이의 값으로 출력
  - 출력의 총합이 1
  - 확률로 계산할 수 있음

![image](https://user-images.githubusercontent.com/83503188/161227861-946e2116-ab82-4758-9a03-da991e3f5e27.png)

#### 출력층의 뉴런 수 정하기
- 분류하고 싶은 클래스 수로 설정
- 이미지를 0부터 9 중 하나로 분류하는 문제라면 출력층의 뉴런을 10개로 설정

