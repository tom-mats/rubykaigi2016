# Fearlessly Refactoring Legacy Ruby

Early success : easy to create the new things
Later succcess : easy to maintain old things

easy to maintain old Ruby?
#
Leagcyコードはプライオリティが低い上にコストがかかる

scara cost

aborb the cost

なぜ，プライオリティが低いのか

* プレッシャーが大きい
  * 時間的
  * 精神的

# コストを下げたい

* Refatoring pattern
* characterization testing
  * legacyコード改善ブック
* A/B Testing

characterziation testingは developement/testingに向いている
A/B testingはproductionに向いている

testdouble/suture

plan -> cut -> record  > validate ? refatoring > verify > compare > fall back > delete

# Plan

# record

* CLIから基準となるデータを記録
* データをDBに保存

# validate

suture.verfyでDBに登録されたデータをもとに正しいか実施

# compare

call_both: ture にすることで両方呼ばれる

# fallbacku

make change safe for users -> 失敗したら古い方のコードを呼ぶ
