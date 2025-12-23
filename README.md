## はじめに
- 本リポジトリは、Java学習者の「Seiya」（Xアカウント： [@Seiya_engineer]( https://x.gd/daily_study)）が作成したMinecraftプラグイン『EnemyDown』に関するものです。
- ご利用いただくことによるトラブル等につきましては、一切の責任を負いかねますことを予めご了承ください。

## ゲーム概要
- Minecraft内で制限時間内に敵を倒し、ポイントを獲得していくことが目的のゲームです。
- 難易度によって、敵の種類と得点は異なり、最終的に獲得した合計のポイントで競います。

## 遊び方

１．コマンドに実施したい難易度を入力します。

　　難易度 easy 「/enemydown easy」

　　難易度 normal 「/enemydown normal」

　　難易度 hard 「/enemydown hard」

２．ゲーム開始時、ネザライトの武器・装具一式が装備され、体力と空腹度が最大に回復されます。

３．制限時間20秒です。エリアに5秒ごとに敵が出現しますので、装備された武器で倒します。

４．ゲーム終了後、点数が表示され、データベースに保存されます。

５．/enemydown listとコマンドを入力すると、過去のスコアを確認できます。

## プレイ動画（easyバージョン）

https://github.com/user-attachments/assets/b56741cf-7af8-4597-b91f-425b6dd1e774


## スコア確認動画

https://github.com/user-attachments/assets/b3cefaac-8f26-4633-b169-9235c2e22d24

## データベース設計　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
|属性　　　　 |設定値　　　 |
|-----|-----|
| データベース名 | spigot_server |
| テーブル名 | player_score | 
