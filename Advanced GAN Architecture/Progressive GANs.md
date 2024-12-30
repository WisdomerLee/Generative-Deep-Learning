# Progressive Growing of GANs
PGGAN

## 기본적인 GAN의 문제

GAN은 적은 데이터 셋의 크기를 갖고 있음, 대개 수백 pixel크기 혹은 100픽셀 미만의 크기의 그림을 생성함

고해상도의 그림을 만드는 것은 GAN 모델에서는 매우 도전적인 일임
generator는 거대한 차원의 데이터 규모를 학습하고, 출력할 수 있어야 하는지를 동시에 배워야 함 - 연산능력이 많이 필요

또한 고해상도로 만들어지는 그림은 세부적인 묘사에서 spot등의 문제로 쉽게 discriminator로 걸러질 수 있고, 이는 훈련 프로세스가 잘 진행되기 어려움을 의미함

1024pixel로 구성되는 거대한 그림의 경우, 메모리 소모량이 매우 많아지고, 현재 GPU 하드웨어가 제공하는 메인 메모리의 한계치에 다다를 정도의 메모리를 소모할 수 있음

추가로, GAN 모델은 역시 여전히 불안정한 학습을 갖고 있으므로, 모델의 훈련 프로세스를 안정화하기 위해 추가로 모델 디자인이 연구되어야 할 필요가 있음

## Progressive Growing
고해상도의 그림을 학습하는 GAN의 훈련의 안정성을 위해 모델 훈련이 진행되는 상황에서 layer들을 점차적으로 늘려가는 과정으로 진행
처음에는 단일 layer로, 그 다음에는 2개의 layer로,... 그리고 그 뒤엔 여러 겹의 deep layer가 쌓인 형태로 만드는 것

Progressive Growing GAN은 generator와 discriminator 모델이 모두 같은 일반 구조를 갖고 있고, 처음에는 매우 작은 이미지부터 시작함 4x4 pixel로 시작

훈련이 진행될 때마다, 새 convolutional layer들이 generator와 discriminator에 둘 다 더해지게 됨

이 상태로 접근하면 고해상도의 품질의 그림을 생성할 수 있게 된다고 함...

Progressive GAN은 저해상도의 그림부터 시작하여 점차 고해상도의 그림으로 만드는 과정을 갖고 있는데, 
처음에는 4x4 -> 그 다음엔 8x8, 과 같은 식으로 2배씩 늘려가며 우리가 원하는 해상도의 그림을 만들 때까지의 과정을 반복 진행 함

각 해상도마다, generator network는 latent space의 내용을 RGB로 바꿔서 그림을 생성하는데, 1x1convolition으로 진행함
만약 4x4에서 8x8의 그림을 만들려고 한다면, latent image를 2배로 키워야 하고, 새 block으로 3x3convolution layer를 추가함
그리고 RGB를 얻기 위한 1x1 layer를 더 추가함
이러한 과정은 residual connection이라고 하여 2배의 scale로 된 4x4 RGB 그림을 늘려나가는 방식으로 적용
residual connection의 weight는 느리게 감소하고, 새 block이 더해지는데 영향을 줌

residual connection의 weight는 alpha라는 값으로 두 layer들 간의 weight를 조정
generator의 해상도는 layer를 통과할 때마다 2배씩 증가함

discriminator는 generator와 완전히 대칭되는 mirror 구조를 갖고 있게 됨
또한 discriminator의 구조 역시 똑같은 형태로 더해지게 됨
