# Hijacking syscalls with (m)Ruby

## Abstract

mrubyを使って，static/shared libraryを作っていろいろhijackしようという話．

mrubyは普通に.oや.aを生成できる&rubyの文法が使えていいよといった話

* mrubyでいろいろやっている
  * SQLの操作(今まで)
  * クラスタリング

## Falut injection

* Chaos Monkey的なツール
  * メモリのシミュレーション
  * デバイスを擬似的に落とす
  　などなど

## なぜするか

* Rubyアプリをよりセキュアにするため

## どうやって置き換えるか

* preload(dlsym)
```
LD_PRELOAD=~.o
```
# mrubyの場合

* Rubyで書ける
* static libraryやshared libraryも作れる
