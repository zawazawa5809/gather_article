# IMPLEMENT フェーズ（執筆＋品質チェック）

#$ARGUMENTS

## 目的

構成案に基づき本文を執筆し、出典・用語・図表の品質を自動検査してドラフトとして保存する。

## 注意事項

- 見出し欠落・順序乖離は自動検知して修正提案を出すこと。
- 用語初出には必ず簡潔定義（括弧）を付すこと。
- すべての主張/数値に脚注`[n]`と出典整合を担保すること。

## 必要な入力ファイル

- `docs/plan/article_plan_{TIMESTAMP}.md`
- 必要に応じて research ファイル

## タスク TODO

1. プラン読込（目標文字数/見出し整合チェック）
2. YAML フロントマター適用
3. 概要（200 字）→ 詳細 → まとめの順に執筆
4. 表/図/画像の挿入（キャプションと出典・ライセンス）
5. 引用・出典の脚注整合チェック
6. 品質スコアリング（100 点満点）
   - 形式(20)/出典(20)/明瞭(20)/正確(20)/可読(20) → 合格基準 80
7. 保存
   - 本文: `docs/drafts/draft_{TIMESTAMP}.md`
   - 品質: `docs/drafts/quality_check_{TIMESTAMP}.md`
8. サマリ出力

## 引数仕様

- **plan**(必須): 構成案パス
- **mode**: new/edit/final（既定 new）
- **quality**: basic/standard/detailed（既定 detailed）
- **output**: draft/final（既定 draft）

## ドラフトテンプレ

---（ユーザー提示の既存ドラフト雛形に準拠し、脚注と図表枠を自動挿入）---

## 品質結果テンプレ

# 品質チェック結果

- スコア: {score}/100（判定: 優良/良好/要改善）
- 形式/出典/明瞭/正確/可読の各評価
- 修正提案 n 件（箇所/提案）

## 最終出力

### 合格

```
status: SUCCESS
next: COMMIT
details: "draft_{TIMESTAMP}.md を保存。品質: {score}/100"
```

### 要修正

```
status: NEED_REVISION
next: IMPLEMENT
details: "quality_check_{TIMESTAMP}.md を参照。"
```
