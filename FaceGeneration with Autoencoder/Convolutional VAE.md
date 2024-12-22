# 그림의 특성을 보다 쉽게 바꾸는 방법
Convolutional VAE
autoencoding의 변주 방식에 Convolution을 적용

훈련으로는 Encoder, Decoder로 훈련을 진행하고

loss는 encoder, decoder의 loss를 모두 고려함

샘플을 만들 때에는 random한 latent point값을 주어 그림을 생성하게 함

# 그림의 특성 바꾸기
특정 특성을 가진 것들이 cluster를 가진 형태로 latent space에 몰려있을 것
그리고 또 그와 반대되는 혹은 대비되는 특성을 가진 것들이 cluster로 몰려있을 것
그러면 그 cluster의 중간(centroid)을 계산
latent space의 공간을 어느 방향으로 움직여야 해당 특성이 나타나는지, 사라지는지를 할 필요가 있음!
그런데 이걸 매번 latent space에서 계산하지 않고, 그냥 빠르게 처리할 수 있을까?

# digit label 같은 것들이 있다면 어떨까?
별다른 구조적인 변화는 없으나, 입력에 label 혹은 attribute를 알려주는 지표(condition)가 추가

그래서 모든 확률 분포 함수가 지표가 추가된 확률분포 함수로 변경

# Attribute-conditioned Image Generation
특성, 조건이 포함된 그림 생성

이제 입력이 encoder로 들어가고, 편차, 표준 등을 기준으로 latent space의 분포로 처리되고, 
decoder로는 attribute가 포함된 vector가 latent space의 값과 함께 들어감!

그러면 특성을 바꾸게 되면 attribute의 vector만 수정하여 decoder로 전달하면 해당 특성이 반영된 그림으로 생성!
