# AIHUB 특허 분야 자동분류 데이터
## Classification 실험
- KoBART
- KoELECTRA
- KorPatELECTRA

위 3개 모델 + 앞으로 특허 분야 디코더 모델 개발하여 성능 비교

### 데이터셋
LLno로 실험 진행, 7개 class들 중 'C'가 76% 차지하는 imbalance dataset

### 기존 문제점
1. ACC, F1-score 0.1점대
2. Train Loss가 Valid Loss보다 낮음

### 해결
1. Imbalance Data이기 때문에 weighted ACC, F1-score metric 사용해야함 -> 사용 후 0.8~0.9점대 기록 중
2. Train Loss가 Valid Loss보다 낮은 이유 중 하나로 의심되는 점 : dropout layer. 해당 레이어는 weights 중 일부를 0으로 만들어 regularization을 진행하지만 Train에서만 사용되고 Valid, Test에서 사용하지 않기 때문에 이 것으로 인한 문제일지도. -> 실험 통하여 비교 예정

### Imbalance Data
- 현재 CrossEntropyLoss 사용 중
- 더 성능 올려보려면 Focal Loss나 Dice Loss 알아보면 좋을 듯.

### 해결 코드
[[PRETRAIN] - process Pretrain data & [AIHUB CLASSIFICATION] - with CrossEntropyLoss](https://github.com/na2na8/PatentSpecification/commit/7922a18c814ca61cf82c733570a9beacc03e05be)