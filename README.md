# LINE DistilBERT Japanese

This is a DistilBERT model pre-trained on 131 GB of Japanese web text.
The teacher model is BERT-base that built in-house at LINE.
The model was trained by [LINE Corporation](https://linecorp.com/).

https://huggingface.co/line-corporation/line-distilbert-base-japanese

## For Japanese

[README_ja.md](./README_ja.md) is written in Japanese.

## How to use

```python
from transformers import AutoTokenizer, AutoModel
tokenizer = AutoTokenizer.from_pretrained("line-corporation/line-distilbert-base-japanese", trust_remote_code=True)
model = AutoModel.from_pretrained("line-corporation/line-distilbert-base-japanese")

sentence = "LINE株式会社で[MASK]の研究・開発をしている。"
print(model(**tokenizer(sentence, return_tensors="pt")))
```

### Requirements

```txt
fugashi
sentencepiece
unidic-lite
```

## Model architecture

The model architecture is the DitilBERT base model; 6 layers, 768 dimensions of hidden states, 12 attention heads, 66M parameters.

## Evaluation

The evaluation by [JGLUE](https://github.com/yahoojapan/JGLUE) is as follows:

| model name             | #Params | Marc_ja | JNLI |       JSTS       |  JSQuAD   | JCommonSenseQA |
|------------------------|:-------:|:-------:|:----:|:----------------:|:---------:|:--------------:|
|                        |         |   acc   | acc  | Pearson/Spearman |   EM/F1   |      acc       |
| LINE-DistilBERT        |   68M   |  95.6   | 88.9 |    89.2/85.1     | 87.3/93.3 |      76.1      |
| Laboro-DistilBERT      |   68M   |  94.7   | 82.0 |    87.4/82.7     | 70.2/87.3 |      73.2      |
| BandaiNamco-DistilBERT |   68M   |  94.6   | 81.6 |    86.8/82.1     | 80.0/88.0 |      66.5      |

## Tokenization

The texts are first tokenized by MeCab with the Unidic dictionary and then split into subwords by the SentencePiece algorithm. The vocabulary size is 32768.

## Licenses

The pretrained models are distributed under the terms of the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

## To cite this work

We haven't published any paper on this work. Please cite [this GitHub repository](http://github.com/line/LINE-DistilBERT-Japanese):

```
@article{LINE DistilBERT Japanese,
  title = {LINE DistilBERT Japanese},
  author = {"Koga, Kobayashi and Li, Shengzhe and Nakamachi, Akifumi and Sato, Toshinori"},
  year = {2023},
  howpublished = {\url{http://github.com/line/LINE-DistilBERT-Japanese}}
}
```