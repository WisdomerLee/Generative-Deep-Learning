# Encoding은 그림의 정보 차원을 축소시키는 과정
Encoding을 통해 그림의 내용이 latent space의 하나의 공간의 위치로 지정

# Latent Decoding을 어떻게 진행하는가?
encoding으로 진행했던 과정을 거꾸로
이번엔 차원을 늘리는 형태로 진행함
물론 이 과정에서 각 neuron에 할당되는 그 값들을 계산하는 것들은 비중치와 bias가 모두 다름
encoding에 쓰인 과정에서 활용되었던 그 값들에 weights와 보정을 추가하여 계산을 시도

복원으로 다시 얻어낸 결과로 얻어진 그림데이터와 입력으로 들어온 그림 데이터를 비교하여 weight를 다시 보정하여 최대한 비슷하게 맞춤
이 과정이 optimize

# 훈련 진행 Training Procedure
입력 데이터는 encoder라는 과정을 forward로 거치며 latent의 표현방식으로 변형
forward pass는 linear algebra의 방식으로 neural layer의 합산으로 진행될 것
latent의 표현방식으로 된 부분은 decode 과정을 forward로 거치며 입력데이터를 최대한 유사하게 복원하려 시도

backpropagation은 network의 weights를 조정하고, network의 에러를 작게 만들어 실제 데이터와 복원된 데이터의 차이를 작게 만들어 줌
