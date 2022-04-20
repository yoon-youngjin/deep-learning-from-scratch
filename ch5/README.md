## ch5 오차역전파법
> 가중치 매개변수의 기울기를 효율적으로 계산하는 방법

- [x] ch4에서 신경망의 가중치 매개변수의 기울기는 수치 미분을 사용해 구했음
- [x] 수치 미분은 단순하고 구현하기도 쉽지만 계산 시간이 오래걸린다는 게 단점 


### 계산 그래프

- [x] 계산 그래프의 특징은 `국소적 계산`을 전파함으로써 최종 결과를 얻는다는 점
- [x] 국소적 계산은 결국 전체에서 어떤 일이 벌어지든 상관없이 자신과 관계된 정보만으로 결과를 출력할 수 있다는 것  
- [x] 전체가 아무리 복잡해도 각 노드에서는 단순한 계산에 집중하여 문제를 단순화할 수 있다는 이점이 있 
- 슈퍼에서 1개에 100원인 사과를 2개 샀습니다. 이때 지불 금액을 구하세요. 소비세가 10% 부과됩니다.

![image](https://user-images.githubusercontent.com/83503188/161944024-1b9cffd5-8a62-4963-8c3c-802aeca4dc1c.png)

- 슈퍼에서 사과를 2개, 귤을 3개 샀습니다. 사과는 1개에 100원, 귤은 1개에 150원입니다. 소비세가 10%일 때 지불 금액을 구하세요.

![image](https://user-images.githubusercontent.com/83503188/161944032-0700a50a-fd6f-4f1e-ab91-ce1961aa8e81.png)
- [x] 덧셈 노드인 ‘+’가 새로 등장하여 사과와 귤의 금액을 합산
- [x] 회로에 전류가 흐르듯 계산 결과가 왼쪽에서 오른쪽으로 전달 => 순전파(forward propagation)



#### 역전파

![image](https://user-images.githubusercontent.com/83503188/161944039-fc9c7538-2fad-427b-84bf-29db871621b1.png)

- [x] 역전파는 순전파와는 반대 방향의 화살표(굵은 선)
- [x] 오른쪽에서 왼쪽으로 ‘1 -> 1.1 -> 2.2’ 순으로 미분 값을 전달
- [x] 해당 결과는 ‘사과 가격에 대한 지불 금액의 미분’ 값 => 사과가 1원 오르면 최종 금액은 2.2원 오른다는 뜻


### 연쇄법칙
> `국소적 미분`을 전달하는 원리

- [x] 계산 그래프의 엣지는 국소적 미분을 기억하고 있다.
- [x] 합성 함수의 미분은 합성 함수를 구성하는 각 함수의 미분의 곱으로 나타낼 수 있다.

![image](https://user-images.githubusercontent.com/83503188/161944047-5e02f98e-e7a2-4109-b39c-ca0135ce2fc3.png)


#### 덧셈 노드의 역전파
- [x] z = x + y
- [x] dz/dx = 1, dz/dy = 1

![image](https://user-images.githubusercontent.com/83503188/161944060-4b06feb6-4bce-4d95-ae00-c1af08aa4381.png)



- [x] 덧셈 노드의 역전파는 입력 값을 그대로 흘려보낸다.

![image](https://user-images.githubusercontent.com/83503188/161944070-54fe7d31-57e8-4885-ae58-ceb6e00301ca.png)



#### 곱셈 노드의 역전파
- [x] z = xy
- [x] dz/dx = y
- [x] dz/dy = x

![image](https://user-images.githubusercontent.com/83503188/161944085-2ccc0493-cccb-4aa7-b184-540ecaa1071c.png)



- [x] 곱셈 노드의 역전파는 상류의 값에 순전파 때의 입력 신호들을 서로 바꾼 값을 곱해서 하류로 보낸다.

![image](https://user-images.githubusercontent.com/83503188/161944092-3e47b86f-dec7-4a75-8439-a98bb1587681.png)


- 사과 쇼핑의 예

![image](https://user-images.githubusercontent.com/83503188/161944109-da5df4e4-8e2c-4585-9c5c-d538b203f096.png)


- [x] 소비세와 사과 가격이 같은 양만큼 오르면 최종 금액에는 소비세가 200의 크기로, 사과 가격이 2.2 크기로 영향을 준다고 해석할 수 있다.
- 사과와 귤 쇼핑의 역전파의 예

![image](https://user-images.githubusercontent.com/83503188/161944126-4fabfcbb-5514-4f41-ba83-2320e7889ec8.png)


### 활성화 함수 계층 구현하기

#### ReLU 계층
- [x] ReLU의 수식

![image](https://user-images.githubusercontent.com/83503188/161946201-d787a3bc-24d1-4b4b-b68b-967f9b7dc05f.png)


- [x] x에 대한 y의 미분

![image](https://user-images.githubusercontent.com/83503188/161946227-4c8a77b1-76eb-494a-836e-5fd74b880476.png)


- [x] 순전파 때의 입력인 x가 0보다 크면 역전파는 상류의 값을 그대로 하류로 흘리고, x가 0이하면 역전파 때는 하류로 신호를 보내지 않음

![image](https://user-images.githubusercontent.com/83503188/161944137-2b8ed6e1-265c-48c4-b6a3-a03f7fd61e21.png)


#### Sigmoid 계층

![image](https://user-images.githubusercontent.com/83503188/161946790-defae857-98d1-4de2-b5f0-051ff4fc672f.png)


- [x] Sigmoid 계층의 계산 그래프(순전파)

![image](https://user-images.githubusercontent.com/83503188/161944145-b9d0ebca-f92c-451d-9e7c-b886d67a8a1e.png)



- [x] `x`, `+` 노드 말고도 `exp`와 `/` 노드가 생김
- [x] exp 노드는 y = exp(x) 계산을 수행, / 노드는 y = 1/x 계산을 수행
- [x] 1단계 
  - [x] `/` 노드, 즉 y=1/x을 미분
  > 상류에서 흘러온 값에 -y^2을 곱해서 하류로 전달

![image](https://user-images.githubusercontent.com/83503188/161944158-9893f3f4-6826-4ce3-b336-757e81254d8a.png)



- [x] 2단계
  - [x] `+` 노드는 상류의 값을 여과 없이 하류로 보냄

![image](https://user-images.githubusercontent.com/83503188/161944170-384738c4-6ab0-4e4e-91c8-169398c2d491.png)


- [x] 3단계	
  - [x] `exp` 노드, 즉 y = exp(x) 을 미분



![image](https://user-images.githubusercontent.com/83503188/161946604-b726ffe3-4080-4725-b00d-b289137d6f50.png)
  > 상류의 값에 순전파 때의 출력(이 예에서는 exp(-x))을 곱해 하류로 전파

![image](https://user-images.githubusercontent.com/83503188/161944181-5c58c9b1-c1f0-4840-b42b-e41edfca2f39.png)






- [x] 4단계
  - [x] `x` 노드는 순전파 때의 값을 서로 바꿔 곱

![image](https://user-images.githubusercontent.com/83503188/161944190-6cef18c5-29bd-483a-864b-34804fba10c5.png)



- [x] 더 간단하게 표현

![image](https://user-images.githubusercontent.com/83503188/161944203-955bf604-8333-4015-82a1-d76e5f9627c0.png)




- [x] 더 간단하게 y로만 표현

![image](https://user-images.githubusercontent.com/83503188/161946936-c5f776bb-b7a9-4b2a-b035-bb1ad2158d87.png)



### Affine 계층
- [x] 신경망의 순전파에서는 가중치 신호의 총합을 계산하기 때문에 행렬의 곱(= np.dot())을 사용

![image](https://user-images.githubusercontent.com/83503188/161947076-9e72e2de-0201-433f-b04d-00c504daafd2.png)

![image](https://user-images.githubusercontent.com/83503188/161944226-8528589e-e06e-4a63-8f0c-232c95a3abce.png)



- [x] 역전파

![image](https://user-images.githubusercontent.com/83503188/161944238-ba574594-6177-4c1d-86ca-50d7c349b516.png)


#### 배치용 Affine 계층

![image](https://user-images.githubusercontent.com/83503188/161947203-b02f34ca-55eb-4403-9eec-cedc5f0ed348.png)


### Softmax-with-Loss 계층
- [x] 출력층에서 사용하는 소프트맥스 함수
- [x] 소프트맥스 함수는 입력 값을 정규화(출력의 합이 1이 되도록 변형)하여 출력
- [x] Softmax 계층은 입력 (a1, a2, a3)를 정규화하여 (y1, y2, y3)를 출력
> CEE 계층은 Softmax의 출력과 정답 레이블(t1, t2, t3)를 받고, 이 데이터들로부터 손실 L을 출력
- [x] Softmax 계층의 역전파는 (y1 – t1, y2 – t2, y3 – t3)라는 말끔한 결과를 내놓는다.
- [x] 신경망의 역전파에서는 이 차이인 오차가 앞 계층에 전해지는 것

![image](https://user-images.githubusercontent.com/83503188/161944256-db7ca4ef-aac5-4a43-a09f-1ab8c42e06f0.png)


### 정리
> 이번 장에서 배운 내용
- 계산 그래프를 이용하면 계산 과정을 시각적으로 파악할 수 있다.
- 계산 그래프의 노드는 국소적 계산으로 구성된다. 국소적 계산을 조합해 전체 계산을 구성한다.
- 계산 그래프의 순전파는 통상의 계산을 수행한다. 한편, 계산 그래프의 역전파로는 각 노드의 미분을 구할 수 있다.
- 신경망의 구성 요소를 계층으로 구현하여 기울기를 효율적으로 계산할 수 있다.(오차역전파법)
- 수치 미분과 오차역전파법의 결과를 비교하면 오차역전파법의 구현에 잘못이 없는지 확일할 수 있다.(기울기 확인) 

