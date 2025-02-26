# PixelCNN
Decoder로 조건을 설정한 그림 생성

global model 

global latent를 이용하여 그림을 생성
다른 부분의 그림을 생성하는 등의 과정은 불가능

global laent를 이용하여 local letent를 생성하고
그 local latent들을 이용하여 그림을 생성
그림의 일부분을 편집하는 과정이 가능

반복적으로 그림을 생성...?
그림의 일정 부분을 만들고, 그 다음을 만들고 하는 과정을 모든 그림 과정에 걸쳐 반복

입력 레이어로 받은 그림의 일부분이 있으면, 첫번째 layer의 특성 맵과 두 번째 layer의 특성맵을 거쳐

input -> [conv 3x3](masked layer A) -> [residual] -> (ReLU)[conv1x1] -> (ReLU)conv[1x1](Softmax)
residual 15개 층으로 구성
residual은
 -> (ReLU)[conv 1x1] -> (ReLU)[conv 3x3](masked layer B) -> (ReLU)[conv 1x1] -> [add]
layer로 구성
add는 residual로 들어온 것과 residual에서 처리한 것을 합침... 

# VQ-VAE
neural discrete representation learning


# Taming Transformers
고화질의 그림 생성 방식

pixel의 codebook이 있어서, Transformer라는 방식으로 ...
다음에 오게 될 pixel을 예측
