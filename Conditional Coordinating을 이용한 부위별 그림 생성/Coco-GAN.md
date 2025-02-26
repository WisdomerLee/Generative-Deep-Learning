# COCO-GAN
global latent space에서 그림을 생성하는 방식이었는데

그림을 보다 세부적으로 원하는대로 편집하기 위해 

그림을 부위별로 특징에 맞는 local latent space에서 생성하는 것

latent vector를 micro coordinate들로 쪼개고, 
각 micro coordinate로 나뉜 것을 가지고 부위별로 그림을 생성한 뒤에

부위별로 생성된 그림을 하나로 맞추는 과정이 들어가는데

COCO-GAN의 동작이 위와 같이 진행됨

위와 같이 진행되면 그림의 품질이 더 고화질이 됨

훈련하는 도중에는 latent space들의 micro coordinate들은 모두 같은 훈련을 받은 상태로 latent space가 동일하게 동작한다고 함??

# In & Out
Diverse Image Outpainting
GAN Inversion

만약 저품질의 그림이 들어왔을 때
이 그림을 고화질로 바꾸고 싶다면 어떻게 해야 할까?

Outpainting via Inversion
non-categorical setting
일부 미완성된 그림이 들어오면 일부 완성된 그림의 부분을

Latent space로 변경하여
최적화된 latent code를 검색하고
각 부위별로 local latent vector가 생성되어, 
각각 그림을 생성하게 하여
그림을 반쪽을 채우도록 실행

local latent vector들을 모아서 별도의 벡터로 만들고

그림을 생성한 뒤에 원본 그림과 다시 생성된 그림을 
비교하여 invert에 활용하는 vector를 학습

categorical setting
일부 미완성된 그림이 들어오면
latent space에서 최적화된 latent code를 찾아서
각각의 latent vector들을 찾아서 
original category와 새 category를 지정하는 값을 추가로 넣어서
그 값을 COCO-GAN이 진행되는 방식처럼 부위별로 그림을 생성하게 하도록 latent vector를 변형

그리고 변형된 latent space들의 벡터들을 이용하여 그림을 생성

# InfinityGAN

기존의 모델과 완전히 다르게 동작함

global latent 부분을 입력 그림에서 획득하면
각 나뉘어진 부분마다 Structure Synthesizer를 거쳐서 
생성된 texture synthesizer를 이용하여 변환

그럼 discriminator는 실제 그림의 일부와 생성된 그림을 가져와서 구분하게 됨

COCO-GAN, SinGAN, SytleGAN+NCI, StyleGAN+NCI+PFG, InfinityGAN

훈련 중에는 resolution을 고정하고, coordinate system도 고정한 상태로 진행함

# SinGAN
Single Natural Image에서 생성하는 모델

먼저 낮은 해상도의 그림을 생성하게 하고, 
점차 높은 해상도의 그림을 생성하게 함
