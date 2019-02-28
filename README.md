## このリポジトリは何？

以下の本を読んで実際にコンパイラを実装してみる。

[低レイヤを知りたい人のための C コンパイラ作成入門](https://www.sigbus.info/compilerbook/#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)

## 開発環境

- Windows10
- Docker for Windows
- gcc
- vscode

---

ここから先は本を読むまで知らなかったこと等を備忘録として書き残す。

## MEMO

### 生成規則

$A → a$
A を 0 個以上の記号 a に展開できるという意味

それ以上展開できない記号を「終端記号」、展開できる記号を「非終端記号」という。
このような生成規則で定義される文法のことを「文脈自由文法」という。

$A → a_1|a_2$
A に複数の展開規則があっても良い。

```
add: mul
add: add + mul
add: add - mul
mul: term
mul: mul * term
mul: mul / term
term: num
term: ( add )
num: digit
num: num digit
digit: 0 | 1 | .... | 9
```

左結合: 左に深くなる(上の例では add + mul の部分)
右結合: 右に深くなる(add: mul + add にする)

### 再帰下降構文解析

トークンをひとつだけ先読みする再帰下降パーサを LL(1)パーサという。
