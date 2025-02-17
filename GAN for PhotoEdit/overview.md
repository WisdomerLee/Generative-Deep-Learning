# 그림 합성, 생성을 위한 neural network

Latent space, Mapping Network, Synthesis Network
w, s등의 하이퍼파라미터

그런데 그림을 어떻게 편집 가능하게 만들 것인가??
생성된 얼굴 그림이 있을 때 다른 부분들의 변경 없이 표정만 바꿀 수 있게 처리하려면 어떻게 해야 하는가??

Latent code > boundary가 있음

InterFaceGAN: Bridging Latent space to attribute space
latent space와 attribute space의 연결

그림을 생성하고, 생성된 그림을 분류하여 다시 반영하는 형태로 진행...

분류를 진행할수록, 생성에 대한 조건을 더 많이 걸 수 있게 됨

random noise에서 Generator로 그림을 생성하면, Feature extractor로 특성들을 뽑아내면, 
뽑혀진 특성들과 그림 생성의 관계를 학습시킴...

다양한 attribute boundary가 latent space를 구분
male-female, young-old, smile-calm,
