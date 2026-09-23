# PROJECT_CONTEXT

## プロジェクト名

楽天トラベル Threads投稿アシスタント

Repository予定名：`rakuten-travel-performance-assistant`

## 目的

楽天トラベルの公式情報をもとにThreads向け紹介文章を作成し、人間が確認・手動投稿した後、その表示・クリック・予約・報酬を記録して改善する。

基本フロー：公式情報を確認 → 旅行情報を登録 → 投稿の切り口を選択 → Threads本文・返信を生成 → 人間が確認 → 手動投稿 → 投稿結果を記録 → 成果を比較して改善。

## 現在Version・Phase

- Version：`Ver.0.1 実運用確認済み`
- Phase：`Ver.0.1 リリース判定`
- 次回再開地点：`Ver.0.1 正式リリース`

## 技術構成

- HTML
- CSS
- Vanilla JavaScript
- localStorage

初期段階ではReact、Vue、Next.js、Node.jsバックエンド、外部DB、認証、サーバー、不要なnpmパッケージを導入しない。ビルド工程を必要としない構成を優先する。

## Ver.0.1主要機能予定

- 旅行情報登録
- 投稿切り口選択
- トーン選択
- 投稿形式選択
- Threads本文生成
- 返信1生成
- 任意の返信2生成
- コピー
- PR表示
- 未確認情報警告
- 投稿候補
- 投稿履歴
- 表示数・クリック・予約成果・報酬の記録
- 投稿形式別比較
- 切り口別比較
- JSONバックアップ・復元

## 保存・選択肢

- localStorage予定キー：`rakutenTravelPerformanceAssistantV1`
- ROOMアプリのlocalStorageキーは使用しない。
- 情報確認状態：`unverified` / `verified` / `expired` / `recheck`
- 投稿形式：`reply_link` / `direct_link` / `multi_reply`
  - 標準：`reply_link`
- 投稿トーン：`natural` / `strong`
  - 標準：`natural`

## 重要ルール

- ROOMアプリを変更しない。
- ROOMデータ・設定・localStorage・デプロイ設定を共有しない。
- Threads自動投稿を実装しない。
- 宿泊経験を捏造しない。
- 未確認の価格・割引・期限を確定情報として生成しない。
- アフィリエイトURLを推測生成しない。
- APIキーを公開JavaScriptへ保存しない。
- 不要な外部ライブラリを追加しない。
- 楽天トラベルAPIの実装・接続・キー設定はPhase 0では行わない。
- Commit・Push・Deploy・GitHubリポジトリ作成は明示指示まで行わない。

## Ver.0.1で実装しないもの

- Threads自動投稿
- X投稿生成、Instagram投稿生成
- 楽天ROOM連携
- 楽天トラベルAPI全面統合
- 自動空室監視・自動価格監視・自動クーポン取得
- ブラウザ自動操作
- ログイン、複数ユーザー
- サーバーDB、クラウド同期

## 開発Phase予定

```text
Phase 0  独立プロジェクト準備・開発基準確定
Phase 1  基本UI・localStorage・旅行情報CRUD
Phase 2  Threads文章生成・コピー
Phase 3  情報確認状態・警告
Phase 4  投稿候補・投稿履歴
Phase 5  成果記録
Phase 6  簡易分析
Phase 7  JSON Export / Import
```

## Phase 0の停止条件

同名プロジェクト、Git管理範囲の不明、ROOM内部への作成可能性、既存ファイルの上書き、仕様との矛盾、削除・移動の必要性、ROOM側の変更必要性が生じた場合は変更せず調査結果と選択肢を報告する。

## Phase 0完了状態

Phase 0では初期ファイルと開発基準を確定した。その後、ユーザーの明示指示によりVer.0.1の一括実装へ進み、現在はローカルブラウザで検証できる状態になっている。

## Ver.0.1実装状況（2026-09-23）

Ver.0.1の一括実装を完了。ローカルブラウザで旅行情報の登録・編集・削除、localStorage保存と再読み込み復元、投稿候補、ルールベースのThreads本文・返信生成、本文・返信編集と個別コピー、投稿準備完了・投稿済み記録、投稿履歴、成果入力、形式別・切り口別の簡易分析、JSON Export / Import、URL形式チェックを実装した。

### データ構造

```text
{
  settings: {},
  candidates: [],
  history: [],
  sales: []
}
```

候補には旅行情報、`status`、`createdAt`、`postedAt`、`metrics`、生成済み投稿を保持する。未入力の成果値は空欄/nullとして扱う。

### 主要関数・UI構成

- `load` / `save`：専用localStorageキーの読み書き
- `generate`：外部AI APIを使わないルールベース文章生成
- `renderCandidates` / `renderHistory` / `renderAnalysis`：画面表示
- `dashboard`、旅行情報登録、投稿候補、投稿履歴、成果確認、バックアップ・設定の6画面

### Ver.0.1 RC最終確認結果（2026-09-23）

架空の「テスト温泉ホテル」を使い、未確認状態の警告、再読み込み復元、本文コピー成功表示、投稿済み記録、成果入力、CTR 2.50%、形式別集計、切り口別集計、最終削除を確認した。strong/naturalの差、direct_linkの本文URL、PR表示、投稿形式・切り口・トーンの保存処理、切り口別ラベル表示を修正して再確認した。JavaScript構文確認と差分空白確認も通過。最終的に架空テストデータを削除し、候補0件・投稿済み0件・クリック0件・予約成果0件・報酬0件を確認した。

### 修正内容・未解決事項

編集画面で入力値が消える不具合、strong/direct_link/確認済み料金の生成反映、投稿メタデータ保存、不正localStorageの無条件上書き、切り口別分析のラベル表示を修正した。ブラウザの確認ダイアログを介した削除操作は確認済み。実ブラウザでのJSONファイル選択によるImport、クリップボード内容の直接照合、スマートフォン実機表示、ブラウザConsoleの直接確認は未実施。

### 次回再開地点

`Ver.0.1 正式リリース`。楽天トラベルAPI、外部AI API、Threads自動投稿は引き続き実装しない。
