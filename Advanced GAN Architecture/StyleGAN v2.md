# StyleGAN을 분석하고, 그림의 품질을 높이기
![image](https://github.com/user-attachments/assets/dca60068-95f2-4538-a5d4-f3cf15fd2ed9)

StyleGAN과 StyleGAN2의 차이는 그림의 품질, 안정성, 등이 그림 품질에 얼마나 영향을 미치는가

## Weight Demodulation
weight demodulation을 도입하여, StyleGAN에서 사용하던 normalization 과정을 대체
이 변화로 StyleGAN에서 만든 그림에서 발생하던 물방울 모양의 흔적들이 사라짐
layer마다 style vector를 계산하고, convolution weight를 modulate
그리고 demodulated를 normalizing으로 나눔
이 weight가 들어가 새 feature map을 만들거나, style을 지정


## Path Length Regularization
훈련의 안정성을 높여줌 - latent space의 path를 정규화
latent space에서 생성되는 그림을 만들 때 보다 안정적이고, 부드러운 변화를 가져다 줌
이 정규화는 훈련 과정을 안정화 시키고, 생성되는 그림의 품질을 좋게 만들어줌


## Revised Architecture
Progressive Growing 기법을 제거하고, 모든 해상도를 훈련시킴
StyleGAN의 가장 큰 특징이었던 progressive growing이라는 것이 고해상도 그림을 얻는데 좋은 역할을 하였으나, 
해당 방식의 구조를 바꾸면서 훈련을 좋게 하는 방법을 고안
ResNet은 일부 연결을 건너뛰는 것으로 했는데, StyleGAN2도 여기서 영감을 얻어, 일부 연결 건너뛰기와 다른 residual 방식을 적용

bilinear filter로 up, downsampling을 하는데 적용함
