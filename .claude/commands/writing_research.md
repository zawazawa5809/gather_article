# RESEARCH フェーズ（web.search による自動リサーチ＆構造化）

#$ARGUMENTS

## 目的

記事の情報収集を自動化し、信頼性評価（情報の確からしさを数値化する簡易指標）と構造化を行う。

## 注意事項

- 常に ultrathink で吟味し、検索ノイズを抑制すること。
- 検索は **web.search**（Web 検索ツールの抽象コマンド）を既定とし、必要に応じて外部 API にフェイルオーバーすること。
- 出典は一次情報（公式発表・規格・論文等）を最優先し、二次情報は補助に限定すること。
- すべての主張・数値に脚注`[n]`を付与し、末尾の参考 URL に整列すること。

## 必要な入力ファイル

- なし（引数のトピックを使用）

## タスク TODO

1. 引数解析（topic, scope, depth, format, time_range, include/exclude_domains, keywords, negative_keywords）
2. クエリ設計（日本語/英語の**ブーリアン**（真偽演算子）最適化、`site:`, `filetype:`, `intitle:`）
3. **web.search**で段階収集（広域 → 絞込 → 一次情報深掘り、期間フィルタ）
4. 信頼性評価（一次性/権威性/整合性/更新性から 10 点満点）
5. 重複除去（URL 正規化（正準化）、タイトル近似、要旨ハッシュ）
6. 構造化カテゴリ {定義/仕様, 公式発表, 実装事例, ベンチマーク, リスク/制約, 競合比較}
7. 文書化 → `docs/research/research_{TIMESTAMP}.md`
8. 次フェーズ引継ぎ JSON（hidden block）を文末に埋め込み
9. コンソールに保存先サマリ出力

## 引数仕様

- **topic**(必須): リサーチ対象
- **scope**: jp/en/both（既定 both）
- **depth**: basic/standard/detailed（既定 detailed）
- **format**: markdown/structured（既定 markdown）
- **time_range**: 期間（例: P18M ＝ 12 か月）
- **include_domains/exclude_domains**: カンマ区切り
- **keywords/negative_keywords**: 追加/除外語

## 出力ファイル

- `docs/research/research_{TIMESTAMP}.md`

## 出力テンプレ

# リサーチ結果: {topic}

## 調査概要

- 調査日時: {ISO8601}
- 検索範囲: {scope} / 深度: {depth} / 期間: {time_range}
- 検索手段: web.search (engine={engine})

## 主要な発見事項

### 1. 定義/仕様

- …

### 2. 公式発表

- …

## 詳細情報

### セクション A

…

## 信頼性評価

- **高**（スコア 7–10）: …
- **中**（5–6）: …
- **要検証**（≤4）: …

## 参考 URL

[1] タイトル — URL — 要旨（100 字）
[2] …

---

```json
{
  "handoff": {
    "recommended_type": "article",
    "audience": "expert",
    "key_messages": ["…"],
    "asset_suggestions": ["表: 仕様比較", "図: アーキテクチャ"]
  }
}
```

## 最終出力

```
status: SUCCESS
next: PLAN
details: "research_{TIMESTAMP}.md に保存。"
```
