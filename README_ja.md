# LINE DistilBERT Japanese

131GBのWebコーパスによって学習された日本語の蒸留BERTモデルです。

https://huggingface.co/line-corporation/line-distilbert-base-japanese

## 概要

このモデルは131GBのWebコーパスで蒸留された日本語DistilBERTです。
モデルはLINE株式会社によって訓練されており、教師モデルには社内で構築したBERT-baseを利用しています。

## 使い方

このモデルはHuggingFaceのtransformersから利用できます。

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

## モデルについて

このモデルは6-layers, 768-hidden, 12-heads, 66Mパラメーターのモデルです。

## 性能評価

[JGLUE](https://github.com/yahoojapan/JGLUE)による評価は以下の通りです。

| model name             | #Params | Marc_ja | JNLI |       JSTS       |  JSQuAD   | JCommonSenseQA |
|------------------------|:-------:|:-------:|:----:|:----------------:|:---------:|:--------------:|
|                        |         |   acc   | acc  | Pearson/Spearman |   EM/F1   |      acc       |
| LINE-DistilBERT        |   68M   |  95.6   | 88.9 |    89.2/85.1     | 87.3/93.3 |      76.1      |
| Laboro-DistilBERT      |   68M   |  94.7   | 82.0 |    87.4/82.7     | 70.2/87.3 |      73.2      |
| BandaiNamco-DistilBERT |   68M   |  94.6   | 81.6 |    86.8/82.1     | 80.0/88.0 |      66.5      |

## トークナイズ

このモデルではまずMeCab+UniDicによる分かち書き後、SentencePieceによるサブワード化が行われます。語彙数は32768です。

## ライセンス

このモデルは[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)にて配布します。

## 引用について

この取り組みは論文になっていません。引用の際は[GitHubリポジトリ](http://github.com/line/LINE-DistilBERT-Japanese)を引用してください。

```
@article{LINE DistilBERT Japanese,
  title = {LINE DistilBERT Japanese},
  author = {"Koga, Kobayashi and Li, Shengzhe and Nakamachi, Akifumi and Sato, Toshinori"},
  year = {2023},
  howpublished = {\url{http://github.com/line/LINE-DistilBERT-Japanese}}
}
```