# CelebFaces Attributes Dataset
20만명의 유명 인사들의 얼굴을 데이터로 가진 데이터 셋, 40개의 특성 annotation을 갖고 있음

이 데이터셋은 여러 컴퓨터 비전 업무에 활용될 수 있는데, 얼굴 형태 인식, 얼굴 인식, 얼굴 감지, 얼굴의 부분 확인, 얼굴 편집, 합성 등의 업무를 맡은 모델의 학습 데이터로 활용될 수 있음

CelebA
각 그림들은 안경, 모자, 턱수염, 미소, 초점, 등등의 특징 들을 갖고 있음

또한 이 데이터는 비상업적, 연구적인 목적에만 활용 가능
img_align_celeba.zip - 그림이 모두 정렬되어있는 얼굴 그림
list_eval_partition.csv - 그림의 학습, 테스트, 평가 데이터 구분
list_bbox_celeba.csv - 각 그림에서 얼굴이 어느 위치에 해당되는지를 알려주는 얼굴 위치 정보가 들어있음
list_landmarks_align_celeba.csv - 그림의 특징과 그 특징의 위치를 알려줌, 왼, 오른쪽 눈, 코, 입의 양끝
list_attr_celeba.csv - 각 그림에 담긴 특징 40개가 담겨있음 - 1은 존재, -1은 존재하지 않음을 알려줌

Convolution VAE
input - encoder - latent - decoder - output

# Image Generation
Convoultion VAE의 과정에서 아래의 부분만 활용하는 것
latent - decoder - output

# Image Interpolation
