# PatentPretrain
- 진행상황 : 체크포인트로 기존 모델들과 AIHUB Classification 성능 측정 ... 미미한 성능 개선 (0.001%) 
- KorPatELECTRA, KoELECTRA도 비슷한 양상 ... 다른 데이터셋에 대해서도 성능 측정 예정
## 문제점
1. checkpoint 저장 시 idx 저장 안 됨 -> DataLoader에서 가공시 전체 데이터 포함 안 하여 idx 변경됨 -> log에 idx 저장하는 방식 -> 다시 처음부터 학습해야 함

# TST
1. 임의로 만든 claim, description : 모두 문장이 큼 -> 4096 토큰 사용할 수 있는 LongFormer 사용
2. claim과 description이 모두 4096이내인 것 개수 확인 중(multiprocessing)
