# ROUGE Score
- [commit : fixed ROUGE Error](https://github.com/na2na8/PatentSpecification/commit/815ac712578cef688c9d3df5939d7832566ebd88)
```python
for idx in range(len(outputs)) :
    for batch_item in range(len(outputs[idx]['preds'])) :
        pred = self.tokenizer.decode(outputs[idx]['preds'][batch_item]) # token_ids를 decode하여 한국어로 변형
        pred = re.sub(r"</s>[\w\W]*", "", pred) # EOS token 이후부터 제거
        target = self.tokenizer.decode(outputs[idx]['targets'][batch_item], skip_special_tokens=True) # token_ids decode하여 한국어로 변형, BOS, EOS, pad 제거
```
- ROUGE 0.5~0.6 정도

# Pre-train : Text Infilling
- BART에서 사용하는 Pretrain objective    
![image](https://user-images.githubusercontent.com/32005272/222957175-0c9ab356-0519-4176-a5d9-0263257c5aca.png)
- 이 중 Text Infilling 사용하기로 함
- Text Infilling은 document의 30% 가량을 masking한다. masking할 span의 길이는 포아송 분포로 정하며, 정해진 후 span은 단일 `<mask>` 토큰으로 바꿔진다.
- RoBERTa처럼 document길이가 길 경우 512토큰을 거의 꽉 채우게 잘라서 학습한다.

1. 문서를 최대 512 토큰 길이로 자른다.
2. 자른 문서의 30% 길이를 마스킹할 길이로 정한다.
3. 해당 길이를 초과할 때까지 포아송 분포로 마스킹 span 길이를 구하고 `<mask>`토큰을 씌운다

