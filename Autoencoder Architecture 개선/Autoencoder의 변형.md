# Autoencoder들의 다양한 변형

input - encoder - latent - decoder - output
이 autoencoder의 기본 뼈대

# latent space
latent space에서 서로 다른 클래스가 멀리 떨어지게 된다면 
서로 다른 클래스를 더 확실히 구분할 수 있음!

그래서 해당 내용을 autoencoder에 적용하면
일반적인 autoencoder는 down sampling(encoder)를 진행하여 같은 latent 공간의 좌표를 up sampling(decoder)로 동작하지만

여기에 변형을 추가하면
latent space에 projection을 진행하는 함수가 latent space에 하나의 좌표가 아니라 확률 분포 형태로 뿌려지고
latent space의 projection으로 생성된 확률분포의 공간에서 임의의 부분을 sampling을 진행하여 up scaling을 진행


Reconstruction loss

Kullback-Leibler divergence

total loss는 reconstruction loss와 kullback-leibler divergence의 weight가 더해진 값을 합쳐 계산함

두 loss를 조합하여 접근

# KL divergence
두 확률분포가 얼마나 다른지를 계산하는 방법
확률분포 하나의 함수에 두 확률분포의 비율을 log값을 취해 곱하여 해당 내용을 적분

변수가 여럿인 일반 분포 P, Q가 있고, 그 확률 분포 함수가 똑같다고 가정하면

Kullback-Leibler divergence 식이 조금 더 간단해지고,

Q의 N이 0과 I사이의 확률분포가 된다면

그럼 이 관계를 통해 loss 값을 계산할 수 있음

확률분포가 얼마나 비슷한지, 다른지를 숫자로 판단할 수 있는 기준이 됨

reconstruction loss값 보정을 매우 크게 잡으면 - 재구축한 그림이 지나치게 서로 멀리 떨어지게 되고...
kl divergence 값의 보정을 매우 크게 잡으면 재구축한 그림의 특성이 제대로 구분이 되지 않음

이 둘의 보정을 적절히 조정하면 latent space에서의 구분이 조금 더 명확해짐

그림의 데이터를 latent vector 분포로
