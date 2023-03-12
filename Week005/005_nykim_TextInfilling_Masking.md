# Text Infilling
1. Tokenizing하여 512 tokens으로 truncation
2. decode하여 스페이스로 단어들 자름
3. 30%까지 masking하도록, span길이 포아송 분포로 하여 진행

[TextInfilling](https://github.com/na2na8/PatentSpecification/tree/main/utils)
