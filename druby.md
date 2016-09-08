# dRuby in the last century

## dRuby以前

* いろいろなオブジェクトをRubyで話したい
  *  RPCではなくRMI
    -> RubyのMethodをSocketで拡張
  * 簡単通信ライブラリではなく，rubyの振る舞いをする何か

＃dRuby

* 分散オブジェクトシステム
  * プロセス越しにmethod call
  * プロセス間でobjectを受け渡し

## サンプル

1. DRb.start_serviceでサービス開始
2. URIのproxy生成
3. アクセスするだけ

+ 暗黙的な公開
  + $stdoutをproxyに変換

## Object指向っぽさ

* 昔はdRuby/RindaでTwitterが実装されていた
* 速度を求めると別の方法に切り替えた
*

##　質疑応答
