# Style GAN
Style-Based Generator 구조

![image](https://github.com/user-attachments/assets/34c171ba-7b37-490e-9b09-862711b676fc)
해당 그림은 Style-Based GAN 논문의 그림을 참고할 것

latent space

입력으로 mapping network라는 f vector라는 것들과 latent space의 내용이 같이 들어가 input이 보정되고, 보정된 input이 network의 구조에 들어감
noise가 추가되는데, 해당 noise는 각 단계에서 들어가 그림의 특성을 추가, 혹은 제거하는데 이용됨

또한 Style GAN은 progressive GAN에 추가적으로 Style을 추가하여 진행되는 구조
style과 중간 중간 noise라는 것을 이용하여 특성을 강조하는 형태로 디테일을 보강하는 형태

## Mapping Network
latent vector를 랜덤하게 지정하고, mapping network가 고려된 latent space로 변환한 뒤
8-layer neural network로 구성되는데, 중간의 latent space의 W 벡터가 생성

## AdaIN
W 벡터는 layer를 통과할 때마다 두 벡터(styles)로 변환되는데, scaling, shifting이 각 layer마다 진행
그리고 normailize와 규모 확장이 진행되는 곳

이 곳에 입력이 들어가기 전에 그림에 다양성을 추가하기 위해 랜덤한 티가 추가됨
또한 mapping network를 거친 값들이 반복적으로 이 곳에 추가됨


## Style Mixing
생성에서 불필요한 연관된 특성이 더해지는 것을 막기 위해 무작위로 각 block들마다 다른 style이 지정됨
latent vector 2개와 연관된 w들은 몇몇 block과의 연관성이 랜덤으로 지정되어 선정됨
여러 형태로 

## Stochastic Variation
중간 중간 들어가는 noise들은 generator가 그림에 변화를 주기 위해 추가되는 것으로, noise도 각 채널마다, 학습된 weight로 부여됨

원래 배운 데이터를 복원하는 것에 그치지 않고 배우지 않은 형태로도 변경을 추가하는 것임

## 세부 묘사는 어떻게 지정?
생성되는 그림의 꼴, 형태, 타입등을 명확하게 지정하기 위해 
synthesis network는 다른 형태의 디테일을 지정할 수 있게 해줌

Coarse - 해상도(4x4- 8x8) - 자세, 머리, 얼굴 형태, 등
Middle - 해상도(16x16 - 32x32) - 구체화된 얼굴의 특성, 머리, 눈동자, 등
Fine - 해상도 (64x64-128x128) - 눈동자, 머리, 살결 색깔, 그리고 그 외 자세한 특성

