# DL

# Neural Network

## SingleLayer Perceptron

![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled.png)

- Input은 기능의 값을 가질 수 있음. 여러 Input에 따른 가중치를 곱함
- 입력값을 곱한 결과를 활성화 함수(Activation Function)로 보냄

![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled%201.png)

- 활성화 함수의 출력 →
    - 입력값의 합이 양수면 1
    - 입력값의 합이 음수면 0
- 만약 입력값이 애초에 0이었다면?
    - 편향(Bias)값을 정의해 더함

![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled%202.png)

## MultiLayer Perceptron

### Activation Function

- `**Sigmoid (시그모이드) 함수**`

입력값을 시그모이드 함수에 넣으면 결과가 0~1 사이의 값을 갖게 된다.

1. **S 자형 곡선**: 시그모이드 함수는 S 자형 곡선을 가지고 있습니다. 이는 입력값이 크게 변할 때 출력값이 빠르게 변화하고, 입력값이 작은 범위에서는 출력값이 둔화됨을 의미합니다.
2. **비선형 함수**: 시그모이드 함수는 비선형 함수입니다. 이는 신경망이 복잡한 데이터를 모델링할 수 있도록 돕습니다. 여러 층의 비선형 활성화 함수를 사용하는 것이 신경망의 표현력을 향상시킬 수 있습니다.
3. **출력 범위**: 시그모이드 함수의 출력 범위는 일반적으로 0과 1 사이입니다. 이는 이진 분류 문제에서 확률 값을 나타내는 데 유용합니다. 출력이 0.5보다 크면 양성 클래스로, 작으면 음성 클래스로 예측할 수 있습니다.
4. **미분 가능성**: 시그모이드 함수는 연속적이며 미분 가능한 함수입니다. 이는 역전파(backpropagation) 알고리즘과 같은 학습 알고리즘에서 사용됩니다.
5. **소멸 그라디언트 문제**: 시그모이드 함수는 입력이 매우 크거나 작을 때 기울기가 0에 가까워지는 문제를 가질 수 있습니다. 이는 역전파 동안 그래디언트 소실 문제를 초래할 수 있습니다.
6. **지수 함수 사용**: 시그모이드 함수는 지수 함수를 사용하므로 계산 비용이 높을 수 있습니다.
- **Gradient Vanishing :** 딥러닝 분야에서 Layer를 많이 쌓을수록 데이터 표현력이 증가하기 때문에 학습이 잘 될 것 같지만, 실제로는 Layer가 많아질수록 학습이 잘 되지 않습니다. 바로 기울기 소실(Vanishing Gradient) 현상때문
    
    역전파 과정에서 [Sigmoid 함수](https://heytech.tistory.com/360?category=453617)의 미분값이 거듭 곱해지면 출력층과 멀어질수록 [Gradient](https://heytech.tistory.com/380) 값이 매우 작아질 수밖에 없습니다.
    
    ![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled%203.png)
    
- `**hyperbolic tangent (하이퍼볼릭 탄젠트) 함수**`
    - **Gradient Vanishing가 있다.**

![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled%204.png)

1. **범위**: 하이퍼볼릭 탄젠트 함수의 출력 범위는 -1부터 1까지입니다. 이는 시그모이드 함수와 비슷하지만, 시그모이드 함수는 0부터 1까지의 범위를 가집니다.
2. **대칭성**: tanh 함수는 0을 중심으로 좌우 대칭입니다. 즉, 입력이 양수일 때 양수 값을 출력하고, 입력이 음수일 때 음수 값을 출력합니다.
3. **비선형성**: 하이퍼볼릭 탄젠트 함수는 비선형 함수로, 입력과 출력 간에 비선형 관계를 나타냅니다. 이는 신경망이 복잡한 데이터를 모델링할 수 있도록 돕습니다.
4. **유도 가능성**: 하이퍼볼릭 탄젠트 함수는 모든 점에서 미분 가능합니다. 이는 역전파(backpropagation)와 같은 학습 알고리즘에서 사용될 수 있습니다.
5. **기울기 포화 문제**: 입력이 큰 절댓값을 가질 때 하이퍼볼릭 탄젠트 함수의 기울기는 0에 가까워집니다. 이는 역전파 동안 그라디언트 소실 문제를 초래할 수 있습니다.
6. **중심 위치**: 하이퍼볼릭 탄젠트 함수는 중심을 0으로 가지므로, 신경망의 출력을 평균이 0인 형태로 만들어주는 효과가 있습니다.

![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled%205.png)

- `**ReLU (렐루) 함수**`
1. **선형 및 비선형**: ReLU 함수는 입력값이 0보다 큰 경우에는 입력값을 그대로 출력하고, 0보다 작은 경우에는 0으로 출력합니다. 이는 입력값에 따라 선형적으로 작동하며, 동시에 입력이 0 이하인 경우 비선형적으로 동작하여 신경망이 비선형성을 표현할 수 있게 합니다.
2. **계산 효율성**: ReLU 함수는 다른 활성화 함수에 비해 계산이 간단하며, 이는 신경망의 훈련 및 추론 과정에서 계산 효율성을 높입니다.
3. **희소성**: ReLU 함수는 입력값이 음수인 경우에는 0을 출력하기 때문에, 출력값이 희소(sparse)하게 됩니다. 이는 일부 뉴런의 비활성화를 통해 희소성을 유지하는 효과를 가져옵니다.
4. **그라디언트 소실 문제 완화**: 시그모이드 함수나 하이퍼볼릭 탄젠트 함수와 같은 활성화 함수가 가진 그라디언트 소실 문제를 완화할 수 있습니다. ReLU 함수는 입력값이 양수인 경우에는 그라디언트가 항상 1이기 때문에 역전파 과정에서 그라디언트 소실 문제가 발생하지 않습니다.
5. **최적화의 용이성**: ReLU 함수는 기울기가 0 또는 1이기 때문에 경사 하강법을 사용하여 모델을 최적화하기 용이합니다.
6. **Dead ReLU 문제**: 입력값이 음수일 때 출력이 0이 되므로, 학습 도중 뉴런이 활성화되지 않을 수 있습니다. 이는 "Dead ReLU"라고 알려진 문제로, 학습 중에 일부 뉴런이 항상 비활성 상태로 남아있을 수 있습니다.

![Untitled](DL%208b9c158a22f04c2eb1a7896aee8a4821/Untitled%206.png)

## Cost Functions