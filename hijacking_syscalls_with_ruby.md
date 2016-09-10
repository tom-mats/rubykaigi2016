# Hijacking syscalls with (m)Ruby

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
