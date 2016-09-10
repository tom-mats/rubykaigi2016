#  Ruby3 concurrency

## Abstract

GuildというConcurrency処理の例，Guild内のProcess/Threadにおいては，並列化はできない．Guildが異なるProcess/Threadにおいては並列化できる．
http://www.atdot.net/~ko1/diary/201609.html#d6

## Use case

Thread内でconcatを使った場合

* MRIだと動く
  * GVLなので全体に排他的制御がかかっており，マルチコアを使って本当の並列処理はしていない．
* JRubyだと動かない
  * 元のJVMがconcatをスレッドセーフな処理として扱っていない．そのため,ruby側でそれを呼び出した場合でも，スレッドセーフではないと判断されアラームが発生する．

## 一般的な並列処理

### Mutexを使う

#### 欠点

* 処理が遅くなる．
* どこにそのような処理をするかは，人に依存してしまい，バグを発生させないようにするのは難しい．
  * mutexが足らない->バグ
  * mutexが多すぎる->処理能力が下がる

### mutable objectを共有しない．(immmutable)

* Elixer/Erlangなど関数型言語で用いられている処理．
* mutable　objectが要求された場合，コピーを渡す．

#### 欠点

* コピー処理は遅い，
* そもそもRubyのオブジェクトはmutableである．それをimmutableにするとなると，互換性が消えてしまう．

## Ruby3の並列処理案(Guild)

* Guild内のThreadは並列処理できない．
* Guild外とのThreadは並列処理できる．
* 他のGuildのオブジェクトには直接は触れない．
  * 専用の処理を通す
    * データのコピー
    * メンバーシップの一時的変更

## メンバーシップの変更

```
g1.transfer_membership(o1) # o1のメンバーシップを変更する．
g2.recieve                 # o1のメンバーシップを取得する．
```

## Immutable objectの取り扱い

* Immutable objectには誰でもアクセスできる，

## 理想的な方法

1. Immutable objectを使う
2. オブジェクトのコピーを使う
3. コピーだと処理が遅い場合は，membershipを変更する
