# Loss
## Cross Entropy Loss
$$
CE = -{1 \over N} \sum_i \sum_{j \in \\{0,1\\}} y_{ij} \log p_{ij}
$$
- $i$ : 몇 번째 데이터
- $j$ : class 수

## Weighted Cross Entropy Loss
$$
WCE = -{1 \over N} \sum_i \alpha_i \sum_{j \in \\{0,1\\}} y_{ij} \log p_{ij}
$$
- $\alpha_i \in [0,1], \log({{n-n_t} \over {n_t}} + K)$
- $n_t$ : # of samples with class t
- $n$ : total # of training set
- K : hparams to tune

## Focal Loss
- $p \in [0,1]$  

$$
FL(p_t)= -(1-p_t)^\gamma \log(p_t)
$$

- $\gamma \in [0,5]$
- $\gamma=0$ -> CE
- $\gamma=2$ -> best
- $\alpha$-balanced

$$
FL(p_t)= -\alpha_t(1-p_t)^\gamma \log(p_t)
$$

## Dice Loss
- Sorensen-Dice coefficient
  - $IoU$ : 교집합 영역 넓이 / 합집합 영역 넓이
  - $Dice = {{2 * |A \cap B|} \over {|A| + |B|}} = {{2 * TP} \over {(TP + FP) + (TP + FN)}}$
  - A : 예측된 모든 positive examples 포함하는 set
  - B : 데이터셋의 모든 golden positive examples
 - $DSC= {{2|A \cap B|} \over {|A| + |B|}} = {{2 \cdot p_{i1} \cdot y_{i1}} \over {p_{i1} + y_{i1}}} = {{2 \cdot p_{i1} \cdot y_{i1} + \gamma} \over {p_{i1} + y_{i1} + \gamma}} (\gamma=1)$ 
 
 $$
 DL = {{1} \over {N}} \sum_i [1 - {{2 \cdot p_{i1}y_{i1} + \gamma} \over {p_{i1}^2 + y_{i1}^2 + \gamma}}]
 $$
 
 ### Self-adjusting Dice Loss
 - soft probability $p$ with decaying factor

$$
DSC(x_i) = {{2(1-p_{i1})^\alpha p_{i1} \cdot y_{i1} + \gamma} \over {(1-p_{i1})^\alpha p_{i1} + y_{i1} + \gamma}}
$$

# ROUGE Score
생성 요약본과 정답 요약본 간 겹치는 n-gram 수를 보는 지표
## Recall & Precision
- Recall = (겹친 단어 수) / (정답 요약본 전체 단어 수)
- Precision = (겹친 단어 수) / (생성된 요약본 전체 단어 수)

## 문제점
- target
  ![image](https://user-images.githubusercontent.com/32005272/221409029-e8f10a59-4f13-4ec6-b7f6-7d76f662f4be.png)
- predict
  ![image](https://user-images.githubusercontent.com/32005272/221409046-d9f0ab0a-526a-4a46-a1f9-64f9ca328145.png)
- 전체 512 토큰에 대해 구하게 되면서 Rouge Score가 0.000~ 점대 기록

## 해결 방안
target Pad 토큰 제외, predict : eos토큰인 </s> 출력 후부터 삭제하여 ROUGE score 계산 -> 0.5점 이상 획득하는 것 확인



