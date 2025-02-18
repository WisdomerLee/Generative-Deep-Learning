# Styleganv2
latent space의 공간에서 특정 공간을 잡아서, 그것을 모습, 형태를 지정하는 것과 맞추게 됨

그럼 이미 학습하지 않고 사용자가 집어넣은 그림을 원하는 방향으로 편집하려면 어떻게 해야 하는가?
사용자가 넣은 그림을 latent space의 공간으로 변경하여야 함...
그리고 latent space에서 위치를 지정하고 변경한 뒤에
그것을 다시 그림으로

latent space의 공간으로 만드는 과정을 inversion
그리고 편집한 뒤에 다시 생성

GAN Inversion: A Survey 논문을 참고하기

그런데 어떻게 사용자의 그림을 latent space의 공간의 벡터로 변형할 수 있는가??

Latent space emgedding for GAN

image alignment

실제로 사용자들이 사용하는 그림은 훈련한 것과 다른 그림일 가능성이 더 큼!!

얼굴을 그림의 중심에 두는 재배치 과정이 필요함

그리고 alignment process는 상대적으로 간단한데, 얼굴의 특징들을 확인
1. 이미 학습된 모델을 토대로 얼굴의 대표 특징을 감지
2. 특징들을 눈, 코, 입 등의 특징들로 맞게 지정
3. bounding box를 지정하고, 크기, 방향 등을 확인
4. 얼굴을 잘라내고 우리가 원하는 해상도의 크기로 변형

