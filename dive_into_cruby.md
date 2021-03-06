# Dive into CRuby

+ New featureを作るには正しいユースケースが必要
  + encodeで正しい読めないデータを置換するというの例では,Web Crawlerを使うことにした
    + Fileなどは，正しいエンコードで読むというのが正しい挙動なのでミスマッチ

* String#encode
  * 文字列のコード変更
* String#scrub
  * 正規表現を用いて置換

pathname.touch
  * rejectされた
  * touchコマンドには複数の意味がある
    * からのファイルを作る
    * ファイルの更新日時を変更する
  * 上記のうちどっちの意味かがわからない．
  * もっと詳細に詰める必要がある

## New platform

* 最近うまく行かなかった例
  * llvm
  * VC++2015

### LLVM

* llvmの方が最適化が激しい
  * GC周りに不具合が出た(使っているのにメモリが解放されてしまった)
* r34278

### VC++2015

* 使っていた構造体メンバが非公開になってしまった．
  * そのメンバを使っている関数から構造体メンバのアドレスを機械語ベースで取ってきた

## パフォーマンスの向上

* ちゃんとボトルネックとなる場所を見つける
  * perf

## Profile

### 遅い場合

* perf-top : どういう関数がどのくらいCPU/Mmeoryを使っているかがわかる
* ObjectSpace
* GC.stat (GCの状態)
* sigdump(Gem)

### 止まっている場合

* Straceだとわからない
  * rubyのコアがthreadの切り替えを求めているけどうまくいかないログだけが残っている
  * procfsを見れば現在実行中のメモリアドレスがわかる
  * 探すのが大変ならpid2line.rb
    * ubuntuだとsudoが必要

### SEGV

+ logは重要なので報告する際は全てコピーして
