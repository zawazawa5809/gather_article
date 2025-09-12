# COMMIT フェーズ（最終化と Git 管理／Windows PowerShell）

#$ARGUMENTS

## 目的

ドラフトを最終配置し、バックアップ作成と Git コミットを自動化する。

## 注意事項

- ファイル名/保存先の自動決定は上書き防止（重複は連番）。
- YAML 必須項目（permalink/title/summary/tags）を検証・補完。
- `#ai-news`タグがある場合は news/、詳細解説は articles/、短報は memo/へ。

## 必要な入力ファイル

- `docs/drafts/draft_{TIMESTAMP}.md`
- `docs/drafts/quality_check_{TIMESTAMP}.md`

## タスク TODO

1. ドラフト検証（YAML/脚注/画像ライセンス）
2. 保存先ディレクトリ決定
3. ファイル名生成 `[YYYY-MM-DD]_{短縮タイトル}.md`
4. 保存＋バックアップ `docs/drafts/backup/`
5. Git 操作（PowerShell）
   ```powershell
   git add .
   git commit -m "[{type}] {title} を追加`n- 記事ID: {permalink}`n- タグ: {tags}`n- 文字数: {chars}"
   ```
6. 成果出力（保存先/バックアップ/コミットハッシュ）

## 引数仕様

- **draft**(必須): ドラフトパス
- **directory**: auto/news/articles/memo（既定 auto）
- **filename**: 明示指定可（未指定は自動）
- **message**: コミットメッセージ（未指定は自動）
- **mode**: immediate/draft（既定 immediate）

## 出力ルール

- docs/news/: `#ai-news`タグあり
- docs/articles/: 技術詳細記事
- docs/memo/: 短報・メモ

## 最終出力

### 成功

```
status: SUCCESS
next: COMPLETE
details: "記事を {dest}/{filename} に保存。Gitコミット完了。記事ID: {permalink}"
files:
  - saved: {fullpath}
  - backup: {backup}
  - commit: {hash}
```

### 失敗

```
status: ERROR
next: MANUAL
details: "{error}。手動対応が必要。"
error_type: [FILE_EXISTS/GIT_ERROR/PERMISSION_ERROR]
suggestion: "対処法"
```
