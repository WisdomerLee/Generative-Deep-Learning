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
## Style Mixing
생성에서 불필요한 연관된 특성이 더해지는 것을 막기 위해 무작위로 각 block들마다 다른 style이 지정됨
latent vector 2개와 연관된 w들은 몇몇 block과의 연관성이 랜덤으로 지정되어 선정됨

## Stochastic Variation
중간 중간 들어가는 noise들은 generator가 보다 사실적인 그림을 만들기 위해 추가되는 것으로, noise도 각 채널마다, 학습된 weight로 부여됨
