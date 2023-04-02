# 사전학습
- HuggingFace `Trainer` -> Custom Scheduler 적용 불가능한 문제(Linear Warmup Scheduler)
- 기존에 사용했던 Pytorch Lightning 사용
- Checkpoint 저장 시 weight만 저장하고 DataLoader 마지막 부분은 저장 안 되어 있는 문제

- last checkpoint에 step수 저장 ... step * batch size만큼 넘어간 곳에서 시작하는 코드로 수정
- Set RandomSeed로 항상 같은 배치 뱉어내는 것 확인
```python
class PretrainDataset(Dataset) :
    def __init__(self, csv_file : str, skiprows : int, trained_rows : int, chunksize : int, num_data : int, tokenizer, state : str, args) :
        self.chunksize = chunksize
        self.csv_file = csv_file
        if state == 'train' :
            self.len = num_data - (skiprows + trained_rows)# 35091902 - (skiprows + trained_rows)
        else :
            self.len = skiprows

        self.chunk_idx = 0
        self.data = pd.read_csv(
            self.csv_file,
            skiprows=1 + skiprows + trained_rows,
            chunksize=self.chunksize,
            names=['idx', 'encoder_input', 'decoder_input'],
            encoding='utf-8',
            encoding_errors='ignore'
        )
```

[Pretrain 코드](https://github.com/na2na8/PatentSpecification/tree/main/pretrain)

# 사전학습 데이터 문제점
- Multiprocessing 적용하지 않음
- 파일을 열고 라인마다 추가하기 때문에 서버 컴퓨터에 느려지는 문제

## 해결 방안
- Multiprocessing 적용
- 100만 라인 씩 리스트에 저장 후 한 번에 추가
