# VAE
VAE 구조에서 다시 출발

그림 생성에는 실제로는 decoder만 쓰임
그렇다면 encoder 과정을 없앤 상태로 decoder만 이용할 순 없을까?

latent space에서 그림을 생성하는 decoder 과정만 남긴다면

그러면 그 상태에서 훈련은 어떻게 시켜야 할까?

기본적으로 해당 상태의 network를 Generative Adversarial Networks(GAN)라고 부름

# Generative Adversarial Networks
random vector에서 Generator model을 통해 가짜 사진, 그림을 만들어냄
실제 데이터도 들어감
진짜와 가짜 데이터가 섞인 데이터를
Discriminator 모델을 통해 주어진 데이터가 진짜인지, 가짜인지 판별함

학습 과정은 두 단계로 진행되는 것이 필요
1. Discriminator 업데이트
2. Generator 업데이트 후 1의 과정으로 돌아감

# Generative Adversarial Networks
Input data - real data

random vector - Generator - fake data
둘이 섞인 data x
y는 진짜인지 가짜인지 쓰인 labels

Discriminator는 들어온 data를 진짜인지, 가짜인지 판별하고, labels를 통해 loss를 확인하여 backprpagation이 진행되어 discriminator 업데이트 진행


Generator는 fake data를 만들어 x와 y에 전달하고, discriminator가 fake data를 판별하게 되면, 
맞출 경우 loss를 확인하고, 해당 내용을 토대로 back propagation을 진행하여 Generator 업데이트 진행

