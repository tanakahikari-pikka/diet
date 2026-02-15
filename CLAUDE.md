# Diet Management System

このディレクトリはhikariのダイエット管理用プロジェクトです。

## 構成

```
diet/
├── CLAUDE.md              # このファイル
├── goals.md               # 目標設定
├── checklist_master.md    # チェックリスト項目マスター（編集用）
├── checklist_initial.md   # 初回診断チェックリスト
├── checklist_weekly.md    # 週間チェックリスト
├── data/                  # CSVデータ
│   ├── weight.csv         # 体重記録
│   ├── meals.csv          # 食事記録
│   └── exercise.csv       # 運動記録
└── logs/                  # 日々の記録（Markdown）
    └── YYYY-MM-DD.md      # 日別ログ
```

## 参照ファイル

> チェックリスト関連の操作時は必ず参照すること

- **[checklist_master.md](./checklist_master.md)** - チェック項目のマスターデータ
  - 項目の追加・変更・削除はここで行う
  - Lv1/Lv2/Lv3 の項目定義とスコア基準を含む

## Claudeへの指示

### 記録の追加

ユーザーが体重、食事、運動を報告したら：

1. **CSVファイルに追記**
   - 体重 → `data/weight.csv`
   - 食事 → `data/meals.csv`
   - 運動 → `data/exercise.csv`

2. **日別ログに記録**
   - `logs/YYYY-MM-DD.md` に追記（なければ作成）

### 分析・レポート

- 「今週の振り返り」→ 直近7日間のデータを集計してサマリー表示
- 「進捗確認」→ 目標に対する現在の達成状況を表示
- 「グラフ」→ CSVデータをもとにASCIIグラフやトレンドを表示

### 入力例

```
今日の体重：72.5kg
朝食：トースト、卵、コーヒー（推定400kcal）
昼食：サラダチキン弁当（500kcal）
夕食：刺身定食（600kcal）
運動：ウォーキング30分
```

このように自然に話しかけるだけでOK。Claudeが適切にパースして記録します。

### コマンド一覧

**記録系**
- `記録して` - 今日の記録を追加
- `今日のまとめ` - 今日の摂取カロリー・消費カロリーを表示
- `今週の振り返り` - 週間サマリー
- `目標を設定` - 新しい目標を設定
- `進捗確認` - 目標に対する進捗を確認

**チェックリスト系**
- `初回診断` - 初回診断チェックリストを実施（checklist_master.md参照）
- `週間チェック` - 週間チェックリストを実施（checklist_master.md参照）
- `項目を追加` - チェックリストに新しい項目を追加（checklist_master.mdを編集）
- `項目を編集` - チェックリストの項目を変更（checklist_master.mdを編集）

### チェックリスト運用ルール

1. **項目の変更**はすべて `checklist_master.md` で行う
2. チェック実施時は `checklist_master.md` を読み込んで最新の項目を使う
3. 結果は `checklist_initial.md` または `checklist_weekly.md` に記録
4. スコア基準も `checklist_master.md` に定義されている
