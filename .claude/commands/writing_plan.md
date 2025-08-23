# PLAN フェーズ（構成設計とテンプレ適用）

#$ARGUMENTS

## 目的

リサーチ結果またはローカル資料から、記事タイプ・読者像・構成・図表を自動設計する。

## 注意事項

- CLAUDE.md の記事ルールを厳格適用。
- 読者価値（**ペイン**（読者の困りごと）→**ゲイン**（得られる価値））を明示。
- 表（テーブル）・図（概念図）・画像は読みやすさに資する場合のみ割当。

## 必要な入力ファイル

- `docs/research/research_{TIMESTAMP}.md` もしくはローカル資料群

## タスク TODO

1. 入力解析（research/ローカル）
2. 記事タイプ自動判定（一次速報 →news／深掘り →article／短報 →memo）
3. ターゲット読者設定（general/expert）
4. 見出し案（最大 3 階層）と要約（200 字）草案
5. 画像/表/コード割当
6. 文体・トーン（である調/ですます調）決定と用語方針
7. CLAUDE.md 準拠チェック
8. 文書化 → `docs/plan/article_plan_{TIMESTAMP}.md`
9. サマリ出力

## 引数仕様

- **input**(必須): research ファイル or カンマ区切りパス
- **type**: news/article/memo/auto（既定 article）
- **audience**: general/expert/auto（既定 general）
- **template**: 自動/指定
- **word_count**: 目標文字数（既定 10000、最小 5000）

## 出力ファイル

- `docs/plan/article_plan_{TIMESTAMP}.md`

## 出力テンプレ

# 記事構成計画: {タイトル案}

## 計画概要

- 作成日時: {ISO8601}
- 記事タイプ: {type}
- ターゲット読者: {audience}
- 目標文字数: {word_count}

## タイトル案

- 案 1 …
- 案 2 …
- 案 3 …

## 見出し構成

1. # 概要（200 字）
2. # 詳細
   ## セクション A
   ## セクション B
3. # まとめ（結論/今後）

## 執筆ガイドライン

- 文体: …
- 用語: 初出に簡潔定義を併記
- 図表方針: …

## キーメッセージ

1. …
2. …
3. …

## 視覚的要素

- テーブル: …
- 図: …
- 画像: …（ライセンス記載）

## YAML フロントマター案

```yaml
---
permalink: /{slug}
title: "{title}"
summary: "{summary}"
tags:
  - "#ai-news"
  - "#{extra}"
---
```

## 品質チェック項目

- [ ] CLAUDE.md 準拠
- [ ] 構成の論理性
- [ ] 出典設計
- [ ] 図表割当
- [ ] 目標文字数整合

## 最終出力

```
status: SUCCESS
next: IMPLEMENT
details: "article_plan_{TIMESTAMP}.md に保存。"
```
