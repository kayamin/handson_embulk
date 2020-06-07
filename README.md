
# Hands ON: Digdag x Embulk

## コンテナを立ち上げる
- digdag x embulk コンテナ
    - digdag, embulk をインストールし，実行するコンテナ
    - target コンテナ の postgresql DB に対して digdag を介して実行された embulk によりデータを insert する
- db コンテナ
    - postgresql を実行するコンテナ

```
docker-compose -up d
```

## embulk が実行できることを確認する
- サンプル生成コマンドを実行して embulk を実行してみる
    - csv ファイルの内容を読み取って，標準出力に出力する

```
docker exec -it digdag_embulk /bin/bash

# embulk のサンプル生成
embulk example embulk_sample/try1

# embulk のタスク定義 config.yml を 入出力情報 seed.yml から自動生成
embulk guess embulk_sample/try1/seed.yml -o embulk_sample/try1/config.yml

# embulk のタスクを dry run
embulk preview embulk_sample/try1/config.yml

# embulk のタスクを実行
embulk run     embulk_sample/try1/config.yml
```

## digdag が実行できることを確認する


```
# digdag ワークフローのサンプル生成
digdag init digdag_sample/mydag

# ディレクトリを移動 digdag はカレントディレクトリに存在するワークフローのみ実行可能なので
cd digdag_sample/mydag

# digdag ワークフローを実行
digdag run mydag.dig
```

## embulk の plugin を導入する

```
# プラグインの独立したバンドルを作成する ( 直下に bundle ディレクトリが生成される)
embulk mkbundle bundle

# gemファイル修正, gem 'embulk-output-command' を追記
vi bundle/Gemfile

# プラグイン追加
cd bundle
embulk bundle install --path=vendor/bundle

# プラグインのインストール状況確認
embulk bundle list

# プラグインの更新
embulk bundle update
cd ../

# config.yml作成
embulk guess -b ./bundle embulk_sample/plugin_sample/seed.yml -o embulk_sample/plugin_sample/config.yml

# プレビュー
embulk preview -b ./bundle embulk_sample/plugin_sample/config.yml

# 実行
embulk run -b ./bundle embulk_sample/plugin_sample/config.yml

```

## digdag から embulk を実行する

