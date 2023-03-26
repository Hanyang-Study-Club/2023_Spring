# Pretrain
- Text Infilling 구현
- 문서 중 16000줄이 넘는 문장이 있어 토크나이징에 시간 걸림 -> 문장 한줄 씩 토크나이징 하여 truncation 하는 방법으로 해결
- 데이터셋 크기가 몹시 크기 때문에 pandas DataFrame의 chunksize 이용하여 메모리 에러 나지 않도록 함

# Text Style Transfer
텍스트 스타일을 바꾸는 태스크, 대표적인 예로 Formal한 문장을 Informal한 문장으로 바꾸는 것, 어떤 작가 스타일의 글을 다른 작가의 글 스타일로 바꾸는 등이 있다.
## [StoryTrans: Non-Parallel Story Author-Style Transfer with Discourse
Representations and Content Enhancing](https://arxiv.org/pdf/2208.13423.pdf)
<img width="880" alt="image" src="https://user-images.githubusercontent.com/32005272/226171887-1d0e762b-529c-4d56-bdf4-0b0fb9fcbb8e.png">

1. $k$ : text style을 담고 있는 단어 사전의 집합
2. $x_m$ : $k$에 해당하는 단어를 masking
3. Encoder로 문맥 벡터를 뽑고, Style Embedding과 concat하여 Fusion Model에 넣어줌
4. 이후 Decoder에 넣어서 masking된 새로운 스타일의 문장 생성
5. $k$와 함께 Encoder, Decoder에 넣어 완벽한 스타일 문장 생성

## Text Style Transfer with CycleGAN
- GAN은 가짜를 생성하는 Generator와 가짜와 진짜를 구별하는 Discriminator로 이루어져 있음.
![image](https://user-images.githubusercontent.com/32005272/226172408-a019fda3-0a24-4038-8267-e40145a34550.png)

- CycleGAN은 Generator로 가짜를 생성하고 다시 Generator로 원래 스타일로 재생성하고, 재생성된 것(Fake)과 원래의 것(Real)을 구별하는 Discriminator로 학습
![image](https://user-images.githubusercontent.com/32005272/226172489-010aabeb-0b6e-49da-bd42-07e1905dec5d.png)

보통 문맥을 Encoder로 뽑고, 뽑아진 벡터를 Decoder로 새로운 스타일을 생성하고 다시 원래 스타일로 재생성함.
![image](https://user-images.githubusercontent.com/32005272/226172651-9a8507f4-5483-4d5b-9913-33cc6c87e4a2.png)



