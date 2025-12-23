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

## データベース構成
|カラム名　　　　 |説明　　 |
|-----|-----|
| id | 主キー、自動採番 |
| player_name | プレイヤー名 |
| score | 倒した敵の得点 |
| difficulty | 難易度 | 
| registered_at | 登録日時 | 

## 工夫したところ
**難易度によって敵の種類と得点を変更し、normal、hardではランダムで敵が出現するようにした。**
- easyはゾンビのみ、normalはゾンビとスケルトン、hardはゾンビ・スケルトン・魔女が出現する設定。
- 難易度に伴い、スケルトンと魔女を倒すと得点が20点加算されるようにした。


- normal、hardではランダムに敵が出現するように設定をおこなった。
  
**可読性を意識したコード設計**
- 各イベントごとにリファクタリングを行い、処理を適切に整理した。さらに、コードの意図が伝わるよう Javadoc でコメントを残し、全体の理解しやすさを向上させた。

## 今後実装予定の機能
- コマンド入力時に設定エリアでゲームをプレイし、終了時に元の場所に戻るようにする。

- ゲーム終了の5秒前にカウントダウンを表示させる。

- Dockerについて学習および導入をして、実行環境を構築する。

## 主な使用技術・環境

| |技術・環境   |
|-----|-----|
| バックエンド |![badge](https://img.shields.io/badge/Oracle%20OpenJDK-21.0.8-grey.svg?style=plastic&logo=openjdk&labelColor=red) |
| アプリケーション |![badge](https://img.shields.io/badge/Minecraft-1.21.8-grey.svg?style=plastic&labelColor=success) |
| サーバー |![badge](https://img.shields.io/badge/Spigot-1.21.8-grey.svg?style=plastic&logo=spigotmc&labelColor=ED8106&logoColor=white) |
| データベース |![badge](https://img.shields.io/badge/MySQL-8.0.44-grey.svg?style=plastic&logo=mysql&labelColor=4479A1&logoColor=white) | 
| 使用ツール |![badge](https://img.shields.io/badge/GitHub-181717.svg?style=plastic&logo=github)&nbsp;![badge](https://img.shields.io/badge/MyBatis-3.5.19-grey.svg?style=plastic&labelColor=DD0700)&nbsp;![badge](https://img.shields.io/badge/intellij%20IDEA-2025.2.3-grey.svg?style=plastic&logo=intellijidea&labelColor=000000)| 

## おわりに
* Java学習者のアウトプットして、リポジトリ公開させていただきました
* 感想・コメント等あればXアカウントまでご連絡くださると幸いです
