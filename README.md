# 楽天トラベル Threads投稿アシスタント

楽天トラベルの公式情報を人間が確認し、旅行情報を整理してThreads向け紹介文章を作成するための専用Webアプリです。投稿は人間が内容を確認し、Threadsへ手動で行う方針です。

## Version・現在Phase

- Version：Ver.0.1 実運用確認済み
- 現在Phase：Ver.0.1 正式リリース

## Ver.0.1の概要

旅行情報の登録、投稿の切り口・トーン・形式の選択、Threads本文と返信の作成、投稿履歴・成果の記録、簡易比較、JSONバックアップ・復元を予定しています。未確認情報を確定情報として扱わないことを重視します。

## 技術構成

HTML / CSS / Vanilla JavaScript / localStorageを使用しています。外部API・ビルド工程は不要です。

## 既存ROOMアプリとの分離

このプロジェクトは、`rakuten-room-post-assistant` とは別の兄弟ディレクトリ、別のGitリポジトリ、別のlocalStorageキーで管理します。ROOMアプリのファイル・設定・データ・デプロイ設定は共有しません。

## 実装済みのVer.0.1機能

旅行情報の登録・一覧・編集・削除、localStorage保存、投稿候補、切り口・トーン・投稿形式の選択、ルールベースのThreads本文・返信生成、文章編集、個別コピー、PR表示確認、未確認情報警告、投稿履歴、投稿済み記録、成果入力、形式別・切り口別の簡易分析、JSONバックアップ・復元、URL形式チェックを実装しています。

## ローカルでの起動方法

プロジェクトフォルダで次のコマンドを実行し、ブラウザで `http://127.0.0.1:8765/index.html` を開きます。

```text
python3 -m http.server 8765
```

または、`index.html`をブラウザで直接開いて利用できます。保存先はブラウザのlocalStorageです。

## 公開版

GitHub Pagesで公開しています。

https://mazemon-rin.github.io/rakuten-travel-performance-assistant/

## 注意事項

文章は外部AI APIを使わないルールベース生成です。Threadsへの投稿は自動化せず、人間が内容を確認して手動投稿します。未確認の価格・割引・期限・空室などは確定情報として生成しません。楽天ROOMアプリとは別プロジェクト・別localStorageキーです。

## 次回

Ver.0.2「楽天トラベルAPI連携設計」へ進みます。APIキーやApplication ID等は、設計・安全確認が完了するまで設定しません。
