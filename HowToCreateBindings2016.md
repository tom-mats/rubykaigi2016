# How to create bindings 2016

* Open SSL Socket YamlはCで実装されたものを使っている
  * つなぐのをBindingという

# GI

* バインディングの自動生成
* GI.load("~") でバインディングできる
  * methodやblockも使える
* 自動的に新しいバージョンが適用される
* 言語によらずメンテナンスできる

# Extenstion library

* 多くのRubyのバンディングはこれで実装されている

# libffi

* FFI(Foregin Function Interface)
* バインディングを実装するためのすべてのAPI(言語によらない)
  * Rubyにはlibffiを呼び出すAPIをFFIと読んでいる

# SWIG

* 専用のiファイル(インクルードファイルが含まれている)を介してバインディングを自動生成
* 何も設定しないと，Rubyっぽくない
* マッピングを用意してあげれば，Rubyぽくなる(コンストラクタなどの関数を設定してあげる)
* 新しいバージョンが出たらビルドし直す必要がある
* 言語毎に設定してあげる必要がある．

OSS Gate/ClearCode booth
