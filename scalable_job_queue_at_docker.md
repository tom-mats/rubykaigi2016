# Scalable job queue system build with Docker

## Job queue

* 遅いタスクを後で実行する処理
* queueにリクエストされたjobを登録
  * Webコンソールでどのように実行されたか確認
  * Railsだとバックエンドを気にせずperfome_laterのいう抽象化されたメソッドを呼び出せば良い

## Data store for queue

よく使われてるもの

* Redis
* RD
* Amazon SQS

## Barbeque

* Cookpads製job queue systemのコア部分
  * Worker
    * Built w serverengine
  * Queue I/F (WebApi)
  * Web console
  * ActiveJobを利用
    * pythonなども使える

### キューのI/F

#### Enqueue

  * Amazon SQSを利用
    * app. job. queue名, message(Hash)

#### Requeue

* サーバ保護のため，delay時間を設定できる

## なぜ新しいジョブキューを作ったか?

* 一部のアプリのみ使っていた
  * kuroko2(closed source，そのうちOSS)というバッチスケジュールシステムがあった
  * 便利なのでJob queueを使うべきでもkuroko2を使ってしまった．

### Job Queue Systemに望むこと

* 集中管理したい
  * たくさんアプリケーションがあり，それ毎にqueueシステムを作ってしまうと管理が大変
* kuroko2風のI/F
* Dockerを使ってscalableにしたい

### Data Store

#### Amazon SQS

* 利点
  * 早い/安定している
  * AWS上なので，AWS上の他のシステムと連携しやすい
* 欠点
  * ジョブの重複が発生するかもしれない(at-least-once QoS)
    * exactly-onceだと,scalable性が下がる．実装が大変

## Worker for execution job

* job queueに登録されている内容を環境変数にしたDockerを呼び出す
  * 'hako' https;//github.com/eagletmt/hako
    * ECSも使える
    * yamlで設定を記載

* Jobの実行時にECSのリソースが足らなかったらAutoscalingする．
* ECSのリソースが余っていたら，クラスターを減らす
