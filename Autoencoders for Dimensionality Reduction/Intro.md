# Latent Spaces
그림을 생성하고 편집하고 그리게 만들어보기를 해보기!

무수히 많은 그림의 정보를 모두 담을 수 없으나, 그림의 내용을 latent space라는 차원 공간의 하나의 위치로 투사할 수 있다면 어떻게 될까?

그림의 내용을 latent space로 투사하는 과정이 E(encoder)
latent space의 위치를 그림으로 변환하는 과정이 D(decoder)

두 그림을 latent space로 각각 encoding하고, 그 위치를 이동시켜가면..?
latent space에서 위치를 변경하여 다시 그림을 만드는 과정을 진행하게 되면 두 그림간 interpolation으로 그림을 만들 수 있게 됨...

그림의 정보는 매우 많은 내용을 담고 있기에 자체 데이터 차원이 매우 큰 편이나, latent space로 사영을 하면 데이터의 차원을 크게 줄일 수 있음

# Image Encoding
그림은 가로, 세로 길이와 픽셀이 색깔 정보를 담고 있음
이 것을 일렬로 늘리는 flattening 과정으로 통해 Input data로 변경
그리고 이 것을 다시 몇 몇 특징 혹은 특성들로 묶게 됨
