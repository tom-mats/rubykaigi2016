

+ FixnumとBignumを廃止して，Integerだけにする(Ruby2.4)
  + 1.classだろうが(2**1000).classだろうがIntegerで返す
  + Fixnum,Bignumという定数は代わりにIntegerを返す．

# 実装の背景

* Fixnumは実装環境によって異なる
* Fixnum/Bignumは国際規格では定義されていない(使ってもいい)
  * Integerはいかなる整数も表現できる
  * subclassを用意して，領域を制限しても制限してもよい
  * Fixnum/Bignum は Common Lisp由来

## なぜ勘違い?
```
irb> 1.class
Fixnum
```

と返ってくるから?

## ドキュメントが簡単になる

* 2.3 まで
  * FixnumとBignumに同じメソッドを実装し，それの説明を書く必要がある
  * ri fooで2つのドキュメントが帰ってくる
* 2.4
  * Integer classまでに定義すればいい

# 欠点

* Integerの領域が不定になる.
  
