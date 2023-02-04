# 概要

- Ruby on Rails の api モードベースのプロジェクトを docker コンテナ内で動かすためのプロジェクト

## 前提

- Ruby on Rails の api モードベースのプロジェクトはサブモジュールとして指定
  - [LeeDDHH/ruby-on-rails-api-mode](https://github.com/LeeDDHH/ruby-on-rails-api-mode)
- Ruby on Rails のプロジェクトを動かす前提として `ruby-image` という Docker イメージをローカルで生成する
  - `yarn ruby:build`
- 本番用・開発用ともに、Docker イメージ作成中に `npm install` をして、 `node_modules` を生成する
- 開発用のみ、PC 側の `backendVolume` のソースを使いながら、コンテナ内に `node_modules` をバインドする
- ruby イメージ用と開発用で `docker-compose.yml` のファイルを分ける
  |用途|ファイル|備考|
  |:---:|:---:|:---:|
  |ruby イメージ用| `docker/ruby_image/docker-compose.yml` | 開発で使うイメージ（ `ruby-image` ）をビルドし、開発用の Dockerfile の基盤とする |
  |開発用| `docker/api/docker-compose.yml` | サブモジュールのプロジェクトを docker コンテナ内の `/usr/app` に配置する |

## 動作環境

### ローカル環境

|                |         |
| :------------: | :-----: |
| Docker Desktop | 4.16.1  |
|      yarn      | 1.22.19 |

### Ruby on Rails 環境

|        |         |
| :----: | :-----: |
|  Ruby  |  3.0.2  |
| bundle | 2.2.22  |
|  gem   |  3.4.5  |
| rails  | 7.0.4.2 |

## コマンド

- プロジェクトを初めて使う場合
  - **必ず `yarn ruby:build` で開発用の Dockefile 用に ruby のイメージ生成する**

### 開発

```shell
# 開発用の Dockefileで使うrubyイメージのビルド
yarn ruby:build

# 開発用のイメージのビルド、コンテナの起動
yarn dev

# 開発用のコンテナの停止
yarn dev:stop

# 開発用のコンテナを起動
yarn dev:start

# 開発用のコンテナの停止とコンテナの削除
yarn dev:down

# 開発用のイメージのビルド
yarn build

# 開発用のコンテナで出力されるログを表示する
yarn log:api
```

### rails コマンド

```shell
# railsのマイグレーション
yarn migrate

# railsのseedを注入
yarn seed

# railsコンソールの起動
yarn console

# railsのルーティングの確認
yarn routes

# railsと連携するDB設定を生成する
yarn db:create
```

### 注意点

- イメージ削除、キャッシュ削除はこまめにする
  - `docker image rm イメージ名`
  - `docker builder prune`
