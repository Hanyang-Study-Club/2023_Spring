# Prompt Learning
![image](https://user-images.githubusercontent.com/32005272/235350735-bb6470cc-d327-461c-abf6-76e7cf50718b.png)

## GPT2
- Pretrain 시 input에 task token을 같이 입력하여 학습함
- 다른 모델과 다르게 각 task마다 fine-tuning하지 않고도 바로 task에 적용할 수 있음

## GPT3
- In-context Learning 시도 : Input을 downstream task를 학습하는 것처럼 넣어주는 것
- 기존 supervised learning은 text와 그에 해당하는 label을 따로 주어서 학습했다면 In-Context Learning의 경우 
- "I'm not the cleverest man in the world, but like they say in French : Je ne suis pa un imbecile"
- 처럼 In French : 뒤의 문장을 generation으로 예측할 때 프랑스어로 번역하는 task를 학습하는 것과 다르지 않다고 함

## Prompt Tuning
Prompt 관련 파라미터를 업데이트하여 학습
- Prefix Tuning : Prefix 부분을 tuning(햑습)하게 됨. 
- PET : Pattern Verbalizer Pair를 이용하여 모델 학습 ( fine tuning)
- P-tuning : Bi-LSTM encoder로 random initializing한 값을 인코딩하여 언어모델에서 MLM한 loss를 사용하여 encoder를 학습  
  ![image](https://user-images.githubusercontent.com/32005272/235351163-6f5c2f24-e415-4647-a356-dddfecee5b75.png)

- Prompt-tuning : input 앞에 soft prompt를 concat하고 soft prompt의 파라미터만을 업데이트
  ![image](https://user-images.githubusercontent.com/32005272/235351231-20c47745-a43d-4e06-9d95-2a950c2538bf.png)

- Pretrained Prompt Tuning : Downstream Task를 grouping하여 Prompt를 사전학습 ... Downstream Task에서 해당 태스크 그룹의 사전학습된 Prompt를 가져와서 사용  
  ![image](https://user-images.githubusercontent.com/32005272/235351189-f3f777f9-be4c-4c52-a852-669af522e8dd.png)
