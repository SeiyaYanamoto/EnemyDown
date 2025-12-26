## はじめに
- 本リポジトリは、Java学習者の「Seiya」（Xアカウント： [@Seiya_engineer]( https://x.gd/daily_study)）が作成したMinecraftプラグイン『EnemyDown』に関するものです。
- ご利用いただくことによるトラブル等につきましては、一切の責任を負いかねますことを予めご了承ください。

## 制作背景
Java およびデータベース技術を用いた処理を実装・検証することを目的に、  
コードの動きを視覚的に確認できる題材として Minecraft を選定しました。

Spigot API を用いて、イベント処理とスコア管理を行うシステムを設計・実装しています。

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

**難易度が上がるにつれて出現する敵の種類が増え、増えた種類の敵はランダムで出現するようにした。**
- easyはゾンビのみ、normalはゾンビとスケルトン、hardはゾンビ・スケルトン・魔女が出現する。
```java
  private EntityType getEnemy(String difficulty) {
    List<EntityType> enemyList = switch (difficulty) {
      case NORMAL -> List.of(EntityType.ZOMBIE, EntityType.SKELETON);
      case HARD -> List.of(EntityType.ZOMBIE, EntityType.SKELETON, EntityType.WITCH);
      default -> List.of(EntityType.ZOMBIE);
    };
    return enemyList.get(new SplittableRandom().nextInt(enemyList.size()));
  }
```

**倒された敵とそれを倒したプレイヤーを取得し、対象リストの敵であればプレイヤーのスコアを敵の種類に応じて加算する。**
```java
  @EventHandler
  public void onEnemyDeath(EntityDeathEvent e) {
    LivingEntity enemy = e.getEntity();
    Player player = enemy.getKiller();

    if (Objects.isNull(player) || spowEntityList.stream().noneMatch(entity -> entity.equals(enemy))) {
      return;
    }

    executingPlayerList.stream()
        .filter(p -> p.getPlayerName().equals(player.getName()))
        .findFirst()
        .ifPresent(p -> {
          int point = switch (enemy.getType()) {
            case ZOMBIE -> 10;
            case SKELETON, WITCH -> 20;
            default -> 0;
          };

          p.setScore(p.getScore()+ point);
          player.sendMessage("敵を倒した！現在のスコアは" + p.getScore() + "点！");
        });
  }
```

## スコア確認動画

https://github.com/user-attachments/assets/b3cefaac-8f26-4633-b169-9235c2e22d24

## データベース設計（ER図）

```mermaid
erDiagram
    Player ||--o{ PlayScore : "1人のプレイヤーは複数の<br>スコアを持つことができる"

    Player {
        int player_id PK "内部ID"
        string uuid UK "Minecraft UUID（識別子）"
        string player_name "現在の表示名"
        datetime registered_at "プレイ日時（登録時刻）"
    }

    PlayScore {
        int score_id PK "スコアID"
        int player_id FK "プレイヤーID"
        int difficulty_id "難易度"
        int score "獲得スコア"
        datetime registered_at "プレイ日時（登録時刻）"
    }
```

※ 本設計における Player は、Minecraft サーバー上で識別されるプレイヤーを指します。

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
* Java学習者のアウトプットして、リポジトリ公開させていただきました。
* 感想・コメント等あればXアカウント[@Seiya_engineer]( https://x.gd/daily_study)までご連絡くださると幸いです。
