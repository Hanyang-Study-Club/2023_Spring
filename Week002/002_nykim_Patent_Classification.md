# AIHUB 특허 분야 자동분류 데이터
## Classification 실험
### 문제점
1. Train Loss가 Validation Loss보다 높은 이유 : Dropout 영향 알아보기
2. Imbalanced Data : 다양한 Loss로 실험해보기

### 결과
1. 첫 epoch에서 Train Loss 0.330, Valid Loss 0.289   
    <img width="342" alt="image" src="https://user-images.githubusercontent.com/32005272/219945375-69899606-1dbb-4cc3-a697-f0e96fd7c9d1.png"><img width="344" alt="image" src="https://user-images.githubusercontent.com/32005272/219945397-d3f478b0-1257-4fe2-886f-224328249ccd.png"> 
    
    -> Regularization? L1, L2? : 사용 안 함. 
    
    -> Dropout? : Dropout portion 0.0으로 해서 실험한 결과 초반엔 Valid가 더 낮은 것으로 나옴. 
    
    -> Training loss is calculated during each epoch, but validation loss is calculated at the end of each epoch  
        ![Train_Loss_is_greater_than_Valid_Loss](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*3WYM__8yle3RLXyJ8SuEiA.png)
        reference : [Your validation loss is lower than your training loss? This is why!
](https://towardsdatascience.com/what-your-validation-loss-is-lower-than-your-training-loss-this-is-why-5e92e0b1747e)

2. 다양한 Loss 적용하기
  - Focal Loss    
      - Focal Loss는 간단히 말하면 Cross Entropy의 클래스 불균형 문제를 다루기 위한 개선된 버전이라고 말할 수 있으며 어렵거나 쉽게 오분류되는 케이스에 대하여 더 큰 가중치를 주는 방법을 사용    
     <img width="347" alt="image" src="https://user-images.githubusercontent.com/32005272/219945807-1467fed8-5cfb-44c4-827f-3eedd1baf486.png"><img width="346" alt="image" src="https://user-images.githubusercontent.com/32005272/219945832-80daf415-dbe2-4524-aa29-938572198da3.png">


  - Dice Loss.   
      <img width="351" alt="image" src="https://user-images.githubusercontent.com/32005272/219946347-0b62b1dd-b2d9-4b7c-bbef-c289e9b1dd31.png"><img width="346" alt="image" src="https://user-images.githubusercontent.com/32005272/219946358-b78eedb0-cc2a-4471-b05c-68d22d70f9e9.png">

### 해결 과제
1. Focal Loss 제대로 이해하지 못해 alpha 값 잘못 넣은 듯, Focal Loss, Dice Loss 정확히 이애하여 다시 적용해보기
2. Learning rate 조정하여 학습 양상 살펴보기
3. Extractive Summarization set 만들기 살펴보기
