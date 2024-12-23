
# Vector Quantized Variational AutoEncoder
Variational Autoencoder는 기본 encoder에 latent space의 변환을 표준 분포에 따른 확률분포로 전환한 것을 기반으로 한 VAE를 기준으로 다시 또 network의 구조를 변경함

VAE에서 latent space에서 그림을 생성할 때
그림의 특성을 변경할 때 latent space의 위치를 변환하여 그 특성이 달라지는 그림을 생성하게 되는데
근본적으로 global latent space를 갖고 있기 때문에, latent space의 각 포인트에서 그림 생성을 시도할 경우
그림을 생성할 때 추가되는 특성의 변경을 시도할 경우, 원본의 그림이 완전히 사라지고 아예 새로운 그림이 생성될 수 있음

그림 자체를 modified 시킬 수 있도록 (그림 전체가 아니라 일부만) 하고 싶음
global latent space를 사용하지 않고, 그림의 일부분만 편집하고 싶다면...?

# VQ-VAE
Encoder로 latent variable을 CNN의 encoder를 통해 latent space의 variable들을 얻어냄 -> CNN을 통해 다시 decoder로 원본 그림을 복원

그러면 latent variable들은 그림의 특성, 특징을 대표하는 vector들이 되는데, 
feature volume이 됨
global latent space가 아니라, 그림에서 추출한 latent variables를 이용하는 것
확률분포로 latent space의 한 포인트로 만드는 것이 아닌, latent variables를 가진 그림 특성을 표현하는 보다 고차원의 특징 vector를 얻어내고, 이 vector에서 그림을 복원하는 것

latent variables에서 일부분만 수정하여, 그 내용을 토대로 그림을 복원 > 그림의 형상을 잃지 않고, 특성만 변경할 수 있음

각 feature의 point들은 각각 chennel의 다른 정보들을 담고 있음
그런데 문제는 이런 feature variables를 많이 담고 있으면, vector의 차원이 매우 커지는 문제가 있음 > 연산이 몹시 매우 많이 필요하므로, 이를 표현할 수 있는 다른 방법이 필요

이것을 극복하는 방안으로 VQ-VAE라는 network가 등장함

제일 먼저 그림에서 vector를 추출함

feature volume의 기준이 되는 dictionary vector를 생성 - 각 vector들은 2차원이고, dictionary vector는 2차원의 vector를 matrix처럼 붙여놓은 것

각 latent pixel은 가장 근처의 dictionary element를 찾음
latent pixel은 dictionary vector의 선형의 합으로 표현될 수 있음 (linear algebra)

# VQ-VAE
dictionary vector를 이용하여
cnn에서 추출된 feature volume은 1channel image이고, 각 pixel의 id를 담고 있음
그럼 어느 특징, 어느 위치를 변경하는지를 확실히 지정할 수 있게 됨

dictionary vector(codebook)을 이용한 vector를 이용하여
encoder로 각각 다른 특성을 가진 것들을 latent space로 변환하였을 때 이들의 거리가 최대한 가깝게 존재하도록 해야 함

decoder도 마찬가지로 ...?

그림 재구성을 통할 때 code vector들의 조합을 어떻게 해야 하는지를 찾아낼 것 (훈련 과정에서)

pixel CNN에서 latent pixel이 얻어지면 embedding space의 기준 vector들이 있고, 
해당 latent pixel에서 embedding space에서의 조합이 어떻게 되는지 관계를 다시 구성한 뒤에 decoder를 통해 그림이 재구성 됨


요약하면 VQ-VAE는 embedding space의 특성의 기준이 되는 vector들을 정해두고,
입력으로 encoder과정을 거치면 나오는 feature volume을 embedding space의 기준 vector들의 조합으로 다시 구성하여
해당 내용을 토대로 decoder에 집어넣어 그림을 재구성하는 것

# VQ-VAE의 encoder, decoder 훈련

그림이 입력되면 encoder로 bottom level, top level로 나누어 encoder가 진행되고
top level에서 VQ로 encoder된 내용이 재구성되면, 그 내용이 bottom level의 latent pixel로 전달되고
bottom level도 역시 VQ로 encoder된 내용이 재구성되어, 해당 내용이 decoder로 들어가 그림을 생성함

level을 둘로 나눈 것은 top level(보다 작은 차원)으로 할 경우 그림의 정보 손실이 있기 때문
이를 보정하기 위해 조금 더 차원이 큰 bottom level을 두어 추가 보정이 진행

그림 생성에는 latent space의 특정에 condition이 추가되어 decoder를 거쳐 그림 생성이 진행
역시 이것의 목적은 재구성된 그림의 품질을 높이기 위함
