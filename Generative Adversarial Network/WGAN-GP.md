# GAN의 문제
GAN(Generative Adversarial Network)은 생성형 임무를 만들 때 실제와 비슷하게 그림, 언어, 음악을 만들어냄

그러나, 사람들이 마주하게 되는 것은 훈련이 매우 불안정하고, 훈련을 시키면 나중엔 generator가 기괴한 생성물을 만드는 것을 볼 수 있음

훈련 과정에서 generator와 discriminator가 각각 경쟁하면서 진행하는데
generator는 점점 discriminator를 속이기 어려워지고, discriminator는 진짜, 가짜를 구분하기 어려워짐

사람들이 discriminator에 바라는 것은 실제 데이터를 잘 걸러내는 것, 그리고 이는
E_x~p_r(x) [log(D(x))] 의 함수를 최대로 만들어야 하며

Generator가 만든 샘플 G(z)는, z~p_z(z)의 discriminator는 D(G(z))의 출력 확률 분포를...최대한 0에 가깝게 만들어야 함
E_z~p_r(z) [log(1-D(G(z)))] 의 함수를 최대로 해야 함

이 두가지 정보를 종합하면 D와 G는 minimax game을 진행함 (한쪽은 최대를, 한쪽은 최소를 만들어야 하는 경쟁 관계)

loss function을 최적화를 해야 할 필요가 있음
min max L(D, G) = E_x~p_r(x) [log D(x)] + E_z~p_r(z) [log(1-D(G(z)))] = E_x~p_r(x) [log(D(x))] + E_x~p_g(x) [log(1-D(x))]

# 또다른 문제 Vanishing gradient
discriminator가 완벽에 가깝게 이를 분리해내면
loss 함수가 0에 가깝게 떨어지고, 훈련을 반복하는 과정에서 gradient의 업데이트가 진행되지 않게 됨 - Generator의 성능 개선이 잘 진행되지 않음

discriminator가 점점 성능이 좋아지면, gradient vanish가 빠르게 진행된다고 함
(비교를 위해 generator는 고정)

GAN의 훈련 딜레마
discriminator가 성능이 나쁘면 Generator가 생성하는 품질이 나빠지게 됨
discriminator의 성능이 좋으면 loss 함수의 gradient가 빠르게 0으로 수렴하여, 훈련 과정이 몹시 매우 느리게 진행됨

# 또다른 문제 Mode collapse
훈련이 진행되면, generator는 항상 같은 결과를 출력하는 상태에 빠질 수 있음
GAN의 실패 사례 중 흔한 것으로, Mode collapse 라고 함

현실의 매우 다양한 사례를 배우는데 실패하고, 소수의 결과에 빠지게 될 수 있음!

# GANs의 또다른 문제 - 좋은 평가 metric이 없음!
GAN은 훈련 과정에서 좋은 함수인지 아닌지 판별하기 어려운 상태의 network
좋은 평가 metric이 없는 상태로 진행하면 깜깜이 훈련이 될 수 밖에 없고, 이를 개선하기도 쉽지 않음
언제 멈춰야 할지 알 수 있는 방법이 없음 - 품질이 가장 좋을 때를 선택할 기준이 애매 - 사람이 눈으로 직접 보는 것 외엔...

# 극복하기 1 Wasserstein -Earth-Mover Distance
기존의 GAN의 loss 함수는 JS divergence로 Pr과 Pg의 분포를 비교

이 metric은 두 분포가 얼마나 다른지를 명확하게 알려줄 수 있는 지표가 없음 즉 둘 사이의 거리 정도는 알 수 있으나, 분포의 형태나 그 외의 것들이 얼마나 차이나는지를 알려줄 수 있는 명확한 지표가 없음, 간접적인 지표는 있을 수 있음

Wasserstein metric은 JS divergence를 대체, 보다 value space가 완만함

Wasserstein Distance는 두 확률 분포의 거리를 계산을 측정하는 또 다른 방법인데
Earth Mover's distance라고도 부름, 하나의 확률분포와 같은 형태의 더미들을 옮기고, 다른 확률분포와 같은 형태로 변경하는데 필요한 최소한의 에너지를 알려줌
각 분포에 해당되는 양을 옮기는 것과 거리를 옮기는 것을 모두 고려하여 선정됨

# Wasserstein - Earth-Mover Distance
서로 다른 분포를 가진 객체로 이동할 때 그 거리가 얼마나 되는지를 확인할 수 있는 방법
하나의 박스 분포에서 다른 박스 분포로 이동할 때 필요한 최소한의 에너지로 그 둘 사이의 거리를 측정
에너지 계산은 얼마나 많은 박스가 옮겨졌는가, 그리고 각 박스가 이동한 거리가 얼마인가를 같이 고려하여 계산됨

둘의 확률 분포를 같은 형태로 옮겨서 각각 얼마나 이동했는지 고려하여 거리를 계산

연속적인 확률분포에서는 해당 내용이 
![image](https://github.com/user-attachments/assets/4ca4df4c-a5ae-4844-a564-f284b5a04138)
Pr, Pg사이에 존재할 수 있는 확률 분포들의 집합
얼마나 많은 퍼센트가 옮겨졌는지를 알려주는 값, x와 y 사이의 거리등
보다 자세한 내용은 Earth-Mover Distance로 확인하기!

# Wasserstein- Earth-Mover Distance
그런데 이것을 정확히 이용하려면, 그 사이에 존재할 수 있는 확률 분포를 모두 고려해야 하는데, 계산의 최적화를 위해서 이것을 변형시킴
자세한 수식은 Wasserstein Metric을 참고할 것
변경된 수식은 K-Lipschitz continuous 를 만족

함수가 K-Lipschitz 연속 함수라고 가정하고,
w라는 파라미터로 정의된 함수라면, 
Wasserstein-GAN의 discriminator의 함수는 실제 데이터와 가짜 데이터의 확률 분포가 얼마나 차이나는지를 학습하게 됨!
그리고 그 차이를 최대로 알 수 있는 함수를 찾으려 할 것
discriminator는 결국 가짜와 진짜를 바로 알려주는 것이 아니라, K-Lipschitz연속함수로 Wasserstein distance를 계산하고, 그 값을 돌려주게 됨

loss 함수가 훈련 과정에서 감소하게 되면 Wasserstein 거리는 충분히 감소하고, generator의 모델이 생성하는 데이터는 실제 데이터의 분포와 비슷해질 것

K-Lipschitz 연속이 훈련 과정중에 보장되어야 하는 것이 있음 -> 즉 weight의 변경으로 함수의 연속성이 깨지는 부분이 발생하면 안 되는 부분이 있음

논문에서 알려주는 현실적인 trick은 모든 gradient의 업데이트가 끝나면 weight를 작은 윈도우를 두어서 parameter space W를 두어서 Lipschitz continuity를 보장하도록 하면 된다고 함

# WGAN-GP
하지만 Wasserstein GAN도 완벽하진 않음
심지어 저자도 논문에서 weight clipping이 필요하여 Lipschitz constraint를 강제하는 것이 좋지 않다고 설명함

WGAN도 불안정한 학습을 보강하기 위해 나왔으나, weight clipping을 거치면 또 문제가 생성됨, clipping indow가 매우 크면, 학습이 느려지고, clipping window가 매우 작으면 vanishing gradient의 문제가 발생
조금 더 나아가서 weight clipping을 gradient penalty와 함께 넣는 방법이 고려됨
