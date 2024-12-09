# Encoding은 그림의 정보 차원을 축소시키는 과정
Encoding을 통해 그림의 내용이 latent space의 하나의 공간의 위치로 지정

# Latent Decoding을 어떻게 진행하는가?
encoding으로 진행했던 과정을 거꾸로
이번엔 차원을 늘리는 형태로 진행함
물론 이 과정에서 각 neuron에 할당되는 그 값들을 계산하는 것들은 비중치와 bias가 모두 다름
encoding에 쓰인 과정에서 활용되었던 그 값들에 weights와 보정을 추가하여 계산을 시도
