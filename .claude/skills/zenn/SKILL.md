---
name: zenn
description: Zennの記事・本を操作するスキル。記事の作成、一覧表示、編集、プレビュー、公開設定などを行う。「記事を作りたい」「Zennの記事を一覧」「記事を公開」などのリクエストで使用。
argument-hint: [action] [options]
---

# Zenn コンテンツ管理スキル

ユーザーのリクエストに応じて、Zenn CLIを使った記事・本の操作を行う。

## 利用可能なアクション

引数 `$ARGUMENTS` に応じて以下を実行する。引数が空の場合はユーザーに何をしたいか確認する。

### 記事の作成 (new, create, 作成, 新規)

```bash
npx zenn new:article
# オプション指定も可能
npx zenn new:article --slug <slug> --title <title> --type <tech|idea> --emoji <emoji>
```

- ユーザーがタイトルやトピックを指定した場合、記事ファイル作成後にフロントマターを編集して反映する
- slugは半角英数字・ハイフン・アンダースコアのみ、12〜50文字
- ユーザーがslugを指定しない場合はZenn CLIの自動生成に任せる

### 記事のフロントマター

記事ファイルの先頭に以下のYAMLメタデータを設定する：

```yaml
---
title: "記事タイトル"
emoji: "😸"          # アイキャッチ（1文字の絵文字）
type: "tech"         # tech: 技術記事 / idea: アイデア記事
topics: ["topic1"]   # タグ（最大5つ、半角英数字・小文字）
published: false     # true で公開
published_at: ""     # 公開日時指定（任意）"YYYY-MM-DD" or "YYYY-MM-DD hh:mm"（JST）
---
```

### 記事の一覧 (list, 一覧)

`articles/` ディレクトリ内のマークダウンファイルを読み取り、タイトル・公開状態・トピックなどを一覧表示する。

### 記事の編集 (edit, 編集)

指定された記事ファイルのフロントマターや本文を編集する。

### 記事の公開 (publish, 公開)

指定された記事の `published: false` を `published: true` に変更する。
実際の公開はGitHubへのpush後にZenn側で反映される。

### プレビュー (preview, プレビュー)

```bash
npx zenn preview
# ポート指定
npx zenn preview --port 3000
```

ローカルでプレビューサーバーを起動する。デフォルトは http://localhost:8000 。

### 本の作成 (new:book, 本)

```bash
npx zenn new:book
npx zenn new:book --slug <slug>
```

### CLIアップデート (update, アップデート)

```bash
npm install zenn-cli@latest
```

## 注意事項

- 記事ファイルは `articles/` ディレクトリに配置される
- 本は `books/[book-slug]/` ディレクトリに配置される
- topicsは半角英数字の小文字で指定する（例: `react`, `nextjs`, `typescript`）
- GitHubにpushすることでZennに反映される
- 画像は `/images/` ディレクトリに配置し、記事からは `/images/ファイル名` で参照できる
