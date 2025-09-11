## How to use

### 1) リサーチ

/project:writing_research topic="Claude Code のサブエージェント" scope=both depth=detailed time_range=P18M engine=bing

### 2) 計画

/project:writing_plan input="docs/research/research_20250820_231500.md" type=auto audience=expert word_count=6000

### 3) 執筆

/project:writing_implement plan="docs/plan/article_plan_20250820_232010.md" quality=detailed output=draft

### 4) コミット

/project:writing_commit draft="drafts/draft_20250820_233200.md" mode=immediate
