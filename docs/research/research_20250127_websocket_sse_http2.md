# リサーチ結果: WebSocket vs HTTP/2 + SSE 技術比較ガイド

## 調査概要

- 調査日時: 2025-01-27T10:00:00+09:00
- 検索範囲: both (日本語/英語) / 深度: detailed / 期間: 2024-2025年
- 検索手段: WebSearch API
- トピック: WebSocket vs HTTP/2 + Server-Sent Events (SSE) の選択基準と技術比較

## 主要な発見事項

### 1. 定義/仕様

#### WebSocket (RFC 6455)
- **プロトコル仕様**: 2011年12月にIETFによってRFC 6455として標準化[1]
- **通信方式**: 単一のTCP接続上での全二重通信チャネルを提供[1]
- **接続方式**: HTTP Upgradeヘッダーを使用してHTTPプロトコルからWebSocketプロトコルへ切り替え[1]
- **ポート**: HTTP/HTTPSと同じポート（80/443）で動作可能[1]

#### Server-Sent Events (SSE) 
- **標準化**: HTML5仕様の一部としてW3C/WHATWGで標準化[2]
- **通信方式**: サーバーからクライアントへの単方向通信[2]
- **API**: EventSource APIを使用してイベントストリームを受信[2]
- **データ形式**: UTF-8エンコードのテキストデータのみ（バイナリ非対応）[2]

#### HTTP/2 (RFC 7540)
- **標準化**: 2015年5月にRFC 7540として公開[1]
- **多重化**: 単一のTCP接続上で複数のストリームを同時処理[3]
- **SSEへの影響**: 従来の接続数制限（6接続/ドメイン）を解消[3]

### 2. パフォーマンス比較（2024-2025年最新ベンチマーク）

#### スループット性能
- **WebSocket**: 最大300万イベント/秒（約400 MiB/s）を達成[4]
- **SSE**: 同様に300万イベント/秒まで到達可能[4]
- **CPU効率**: WebSocketはSSEより若干低いCPU使用率で高スループット実現[4]

#### レイテンシ比較
- **WebSocket**: 全二重通信により最低レイテンシを実現[5]
- **SSE**: 単方向通信のためサーバー→クライアント方向のみ低レイテンシ[5]
- **実用目標値**: 50msレイテンシで10万イベント/秒が実用的な目標[4]

### 3. 接続制限とHTTP/2の影響

#### HTTP/1.1での制限
- **SSE接続制限**: ブラウザあたり6接続/ドメイン（複数タブ使用時に問題）[3]
- **ブラウザ対応**: Chrome、FirefoxともにHTTP/1.1での制限は「Won't fix」扱い[3]

#### HTTP/2での改善
- **多重化**: 単一TCP接続上で最大100ストリーム（デフォルト）まで同時処理[3]
- **制限解消**: HTTP/2使用時はSSEの6接続制限が事実上解消[3]
- **ブラウザサポート**: 全世界ユーザーの97.16%がHTTP/2対応ブラウザを使用[5]

## 詳細情報

### セクション A: ユースケース別選択ガイド

#### WebSocketを選ぶべきケース
1. **チャットアプリケーション**: 双方向のリアルタイムメッセージング[6]
2. **オンラインゲーム**: 低レイテンシの双方向通信が必須[6]
3. **コラボレーションツール**: 複数ユーザー間のリアルタイム同期[6]
4. **インタラクティブダッシュボード**: ユーザー操作を伴うリアルタイム更新[6]
5. **IoT（双方向）**: デバイスからのデータ送信と制御コマンド受信[7]

#### SSEを選ぶべきケース
1. **株価ティッカー**: サーバーからの一方向データプッシュ[6]
2. **ニュースフィード**: 継続的なコンテンツ更新配信[6]
3. **監視ダッシュボード**: Netflix Hystrixのようなパフォーマンスメトリクス配信[7]
4. **通知システム**: サーバー起点のイベント通知[7]
5. **ライブコメンタリー**: スポーツ実況など一方向の情報配信[7]

### セクション B: 技術的特徴比較

#### データ形式サポート
- **WebSocket**: バイナリデータとUTF-8テキストの両方をサポート[5]
- **SSE**: UTF-8テキストのみ（バイナリ非対応）[5]

#### 自動再接続機能
- **WebSocket**: 組み込みの再接続機能なし（追加実装が必要）[5]
- **SSE**: 自動再接続、イベントID、任意イベント送信機能を標準装備[5]

#### 実装の複雑さ
- **WebSocket**: 専用プロトコルとサーバー実装が必要[5]
- **SSE**: 通常のHTTP上で動作、curlでのテストも可能[5]

### セクション C: セキュリティ考慮事項（2024年最新）

#### WebSocketセキュリティ
1. **CSRF対策**: トークンベース認証（JWT）の使用を推奨[8]
2. **XSS対策**: 入力検証とサーバー側サニタイズが必須[8]
3. **認証**: ハンドシェイク時だけでなくメッセージごとの認証チェック[8]
4. **暗号化**: 常にWSS（WebSocket Secure）を使用[8]

#### SSEセキュリティ
- HTTPベースのため標準的なWebセキュリティ対策が適用可能
- CORSポリシーによるオリジン制御が容易

## 信頼性評価

### 高信頼性情報源（スコア 8-10）
- **RFC 6455（WebSocket仕様）**: IETF公式標準文書 [スコア: 10]
- **RFC 7540（HTTP/2仕様）**: IETF公式標準文書 [スコア: 10]
- **MDN Web Docs（SSE/EventSource）**: Mozilla公式ドキュメント [スコア: 9]
- **W3C/WHATWG仕様**: Web標準化団体公式文書 [スコア: 9]

### 中信頼性情報源（スコア 6-7）
- **Timeplus社ベンチマーク（2024）**: 実測データ付き技術記事 [スコア: 7]
- **Ably社技術ブログ（2024）**: 専門企業による比較分析 [スコア: 7]
- **Stack Overflow回答**: コミュニティベースの実装経験 [スコア: 6]

### 要検証情報（スコア ≤5）
- **個人ブログ記事**: 主観的意見や限定的な経験 [スコア: 4]
- **古い記事（2020年以前）**: 技術進化により陳腐化の可能性 [スコア: 3]

## 実装推奨事項

### 2025年における選択基準

1. **双方向通信が必要** → WebSocket一択
2. **単方向通信で十分** → SSE（HTTP/2環境）を優先検討
3. **バイナリデータ送信** → WebSocket必須
4. **実装シンプルさ重視** → SSE推奨
5. **最大パフォーマンス** → WebSocket（CPU効率優位）
6. **自動再接続重要** → SSE（標準機能）
7. **レガシーブラウザ対応** → WebSocket（より広範なサポート）

### インフラ要件

- **HTTP/2対応**: SSE採用時は必須（接続制限回避のため）
- **プロキシ/ファイアウォール**: WebSocketは特別な設定が必要な場合あり
- **ロードバランサー**: WebSocketは sticky session設定推奨

## 参考URL

[1] RFC 6455 - The WebSocket Protocol — https://datatracker.ietf.org/doc/html/rfc6455 — WebSocketプロトコルの公式仕様書。IETFによって2011年に標準化された全二重通信プロトコルの詳細定義。

[2] Server-sent events - Web APIs | MDN — https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events — Mozilla開発者向けドキュメント。SSEとEventSource APIの使用方法と仕様詳細。

[3] Is there still a practical 6 connection limit when using Server Sent Events with HTTP2? — https://stackoverflow.com/questions/59163596/ — HTTP/2環境でのSSE接続制限に関する技術的議論と解決策。

[4] WebSocket vs. Server-sent Events: A Performance Comparison — https://www.timeplus.com/post/websocket-vs-sse — 2024年のTimeplusによる詳細なパフォーマンスベンチマーク結果。

[5] WebSockets vs Server-Sent Events: Key differences and which to use in 2024 — https://ably.com/blog/websockets-vs-sse — Ably社による包括的な技術比較と選択ガイド。

[6] Server-Sent Events vs WebSockets – How to Choose — https://www.freecodecamp.org/news/server-sent-events-vs-websockets/ — freeCodeCampによるユースケース別の選択指針。

[7] Real-Time Updates in Web Apps: Why I Chose SSE Over WebSockets — https://dev.to/okrahul/real-time-updates-in-web-apps-why-i-chose-sse-over-websockets-k8k — 実装者視点でのSSE選択理由と実例。

[8] WebSocket security: How to prevent 9 common vulnerabilities — https://ably.com/topic/websocket-security — 2024年最新のWebSocketセキュリティベストプラクティス。

---

```json
{
  "handoff": {
    "recommended_type": "article",
    "audience": "expert",
    "key_messages": [
      "HTTP/2環境ではSSEが従来の接続制限を克服し実用的な選択肢に",
      "WebSocketは双方向通信とバイナリデータ送信で依然として優位性",
      "2025年現在、用途に応じた適切な技術選択が重要",
      "セキュリティ面ではトークンベース認証と入力検証が必須"
    ],
    "asset_suggestions": [
      "表: WebSocket vs SSE 機能比較マトリクス",
      "図: ユースケース別技術選択フローチャート",
      "図: HTTP/1.1 vs HTTP/2でのSSE接続モデル比較",
      "表: パフォーマンスベンチマーク結果サマリー"
    ]
  }
}
```