---
permalink: /websocket-vs-sse-http2-complete-guide-2025
title: "【2025年最新】WebSocket vs HTTP/2 + SSE 完全選択ガイド：技術者のための実装判断フローチャート付き"
summary: "リアルタイム通信技術の選択に迷う技術者向けに、WebSocketとSSE+HTTP/2の性能実測値、ユースケース別の判断基準、セキュリティ考慮事項を網羅的に解説。判断フローチャートと実装例付きで、即座に技術選定が可能。"
tags:
  - "#websocket"
  - "#server-sent-events"
  - "#http2"
  - "#real-time-communication"
  - "#performance"
  - "#security"
  - "#2025-trends"
  - "#technical-guide"
  - "#architecture"
  - "#web-development"
---

# 【2025年最新】WebSocket vs HTTP/2 + SSE 完全選択ガイド：技術者のための実装判断フローチャート付き

## はじめに：なぜ今、WebSocketとSSEの選択が重要なのか

2025年のWebアプリケーション開発において、リアルタイム通信技術の選択は以前にも増して重要になっている。多くの技術者が「とりあえずWebSocketを使えば良い」という安易な選択をしているが、HTTP/2の普及により、SSE（Server-Sent Events）が従来の制限を克服し、実用的な選択肢として再浮上している[1]。本記事では、最新のパフォーマンス実測値と実装経験に基づき、WebSocketとSSE+HTTP/2の適切な使い分けについて、判断フローチャートと具体的な実装例を交えて解説する。読者は本記事を通じて、技術選択の迷いから解放され、プロジェクトに最適な通信技術を自信を持って選択できるようになる。

## 3つの技術の基本理解

### WebSocket：全二重通信の王道

WebSocket（ウェブソケット）は、2011年12月にIETFによってRFC 6455として標準化された、単一のTCP接続上で全二重通信を実現するプロトコルである[1]。最大の特徴は、クライアントとサーバーが同時に双方向でメッセージを送受信できることだ。

WebSocketの接続確立は、通常のHTTPリクエストから始まる。クライアントがHTTP Upgradeヘッダーを含むリクエストを送信し、サーバーが101 Switching Protocolsレスポンスを返すことで、HTTPからWebSocketプロトコルへの切り替えが行われる[1]。この仕組みにより、HTTP/HTTPSと同じポート（80/443）での動作が可能となっている。

```javascript
// WebSocketクライアント実装の基本パターン
const ws = new WebSocket('wss://example.com/socket');

ws.onopen = (event) => {
    console.log('接続確立');
    ws.send(JSON.stringify({ type: 'greeting', message: 'Hello Server' }));
};

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('受信データ:', data);
};

ws.onerror = (error) => {
    console.error('WebSocketエラー:', error);
};

ws.onclose = (event) => {
    console.log('接続終了', event.code, event.reason);
};
```

WebSocketのデータフレームは、テキストとバイナリの両方をサポートしており、画像や動画などのバイナリデータを効率的に送信できる[2]。これはSSEには無い重要な利点である。

### SSE（Server-Sent Events）：シンプルな単方向通信

SSE（Server-Sent Events）は、HTML5仕様の一部としてW3C/WHATWGで標準化された、サーバーからクライアントへの単方向通信技術である[3]。EventSource APIを使用することで、サーバーから継続的にイベントを受信できる。

SSEの最大の特徴は、通常のHTTP接続上で動作することだ。特別なプロトコルやサーバー実装を必要とせず、既存のWebインフラストラクチャとの親和性が高い[3]。

```javascript
// SSEクライアント実装の基本パターン
const eventSource = new EventSource('/events');

eventSource.onopen = (event) => {
    console.log('SSE接続確立');
};

eventSource.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('受信データ:', data);
};

// カスタムイベントの処理
eventSource.addEventListener('custom-event', (event) => {
    console.log('カスタムイベント:', event.data);
});

eventSource.onerror = (error) => {
    console.error('SSEエラー:', error);
    // SSEは自動的に再接続を試みる
};
```

SSEのイベントストリームは、UTF-8エンコードされたテキストデータのみをサポートする[3]。各メッセージは以下のような形式で送信される：

```
data: {"message": "Hello Client"}\n
id: 12345\n
event: custom-event\n
retry: 5000\n
\n
```

SSEは自動再接続、イベントID、任意イベント送信などの機能を標準で備えており、WebSocketでは追加実装が必要な機能が最初から利用できる[4]。

### HTTP/2：SSEの制限を解き放つ多重化技術

HTTP/2は2015年5月にRFC 7540として公開されたプロトコルで、HTTP/1.1の根本的な制限を解決する革新的な技術である[5]。特にSSEとの組み合わせにおいて、その真価を発揮する。

HTTP/1.1環境では、SSEは深刻な接続数制限に直面していた。ブラウザは同一ドメインに対して最大6接続という制限を設けており、複数タブでアプリケーションを開いた場合、すぐに上限に達してしまう問題があった[6]。

HTTP/2の多重化機能により、この制限は事実上解消された。単一のTCP接続上で複数のストリームを同時に処理できるため、デフォルトで最大100個のSSE接続を同時に維持できる[6]。

```
┌─────────────────────────────────────┐
│          HTTP/1.1の場合             │
├─────────────────────────────────────┤
│ ドメイン: example.com               │
│ ┌──────┐┌──────┐┌──────┐         │
│ │SSE #1││SSE #2││SSE #3│         │
│ └──────┘└──────┘└──────┘         │
│ ┌──────┐┌──────┐┌──────┐         │
│ │SSE #4││SSE #5││SSE #6│ ← 限界  │
│ └──────┘└──────┘└──────┘         │
│ ❌ SSE #7 (接続不可)                │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│          HTTP/2の場合               │
├─────────────────────────────────────┤
│ ドメイン: example.com               │
│ ┌─────────────────────────────┐    │
│ │    単一TCP接続（多重化）      │    │
│ │ ┌────┐┌────┐┌────┐...      │    │
│ │ │#1  ││#2  ││#3  │          │    │
│ │ └────┘└────┘└────┘          │    │
│ │ 最大100ストリーム同時処理可能 │    │
│ └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

2025年現在、全世界のWebユーザーの97.16%がHTTP/2対応ブラウザを使用しており[7]、この技術は既に標準となっている。

## パフォーマンス実測値で見る性能差

### スループット比較（2024-2025年ベンチマーク）

最新のベンチマーク結果によると、WebSocketとSSEの両方が最大300万イベント/秒（約400 MiB/s）という驚異的なスループットを達成できることが判明している[8]。これは理論値ではなく、実際の測定結果である。

**表1: スループット性能比較（2024年実測値）**

| 指標 | WebSocket | SSE | 測定条件 |
|------|-----------|-----|----------|
| 最大スループット | 300万イベント/秒 | 300万イベント/秒 | バッチサイズ1000 |
| データ転送速度 | 約400 MiB/s | 約400 MiB/s | 同上 |
| CPU使用率（同一スループット時） | 65% | 72% | 100万イベント/秒時 |
| メモリ使用量 | 512MB | 480MB | 1000接続時 |

興味深いことに、WebSocketはSSEより若干低いCPU使用率で同等のスループットを実現している[8]。この差は、WebSocketの専用プロトコルがHTTPヘッダーのオーバーヘッドを削減しているためと考えられる。

### レイテンシ特性

レイテンシにおいては、WebSocketが明確な優位性を示している。全二重通信により、クライアントからサーバーへのメッセージ送信とその応答を最小限の遅延で実現できる[9]。

```javascript
// レイテンシ測定コード例
class LatencyMeasurement {
    constructor(protocol) {
        this.protocol = protocol;
        this.measurements = [];
    }
    
    measureWebSocket() {
        const start = performance.now();
        const ws = new WebSocket('wss://example.com/ws');
        
        ws.onopen = () => {
            ws.send(JSON.stringify({
                type: 'ping',
                timestamp: Date.now()
            }));
        };
        
        ws.onmessage = (event) => {
            const end = performance.now();
            const latency = end - start;
            this.measurements.push(latency);
            console.log(`WebSocket往復遅延: ${latency.toFixed(2)}ms`);
        };
    }
    
    measureSSE() {
        // SSEは単方向のため、サーバー→クライアントのみ測定
        const eventSource = new EventSource('/sse');
        
        eventSource.onmessage = (event) => {
            const serverTimestamp = JSON.parse(event.data).timestamp;
            const latency = Date.now() - serverTimestamp;
            this.measurements.push(latency);
            console.log(`SSE遅延: ${latency}ms`);
        };
    }
}
```

実測値では、WebSocketの往復遅延が平均15-25ms、SSEのサーバー→クライアント遅延が10-20msという結果が得られている[9]。実用的な目標値として、50msのレイテンシで10万イベント/秒の処理が推奨される[8]。

### スケーラビリティ

接続数の限界値について、両技術には明確な違いがある。

**表2: 接続数スケーラビリティ比較**

| 環境 | WebSocket | SSE (HTTP/1.1) | SSE (HTTP/2) |
|------|-----------|----------------|--------------|
| 同一ドメイン最大接続数 | 理論上無制限* | 6接続 | 100接続（デフォルト） |
| サーバー側制限 | OSのファイルディスクリプタ数 | 同左 | 同左 |
| 実用的な同時接続数（単一サーバー） | 10,000-50,000 | 10,000-50,000 | 10,000-50,000 |

*実際にはブラウザやネットワーク機器の制限を受ける

HTTP/2環境下では、SSEの6接続制限が解消され、実用上十分な100接続まで同時利用が可能となる[6]。これにより、マルチタブ対応のダッシュボードアプリケーションなどでも問題なく動作する。

## ユースケース別の技術選択フローチャート

### WebSocketが必須のケース

以下のユースケースでは、WebSocketの採用が強く推奨される：

**1. チャットアプリケーション**
双方向のリアルタイムメッセージングが必須であり、タイピングインジケーターやリアクションなど、即座の応答が求められる[10]。

```javascript
// チャットアプリのWebSocket実装例
class ChatClient {
    constructor(userId) {
        this.userId = userId;
        this.ws = new WebSocket('wss://chat.example.com');
        this.setupHandlers();
    }
    
    setupHandlers() {
        this.ws.onmessage = (event) => {
            const message = JSON.parse(event.data);
            switch(message.type) {
                case 'message':
                    this.displayMessage(message);
                    break;
                case 'typing':
                    this.showTypingIndicator(message.userId);
                    break;
                case 'presence':
                    this.updateUserPresence(message);
                    break;
            }
        };
    }
    
    sendMessage(text) {
        this.ws.send(JSON.stringify({
            type: 'message',
            userId: this.userId,
            text: text,
            timestamp: Date.now()
        }));
    }
    
    sendTypingStatus(isTyping) {
        this.ws.send(JSON.stringify({
            type: 'typing',
            userId: this.userId,
            isTyping: isTyping
        }));
    }
}
```

**2. オンラインゲーム**
低レイテンシの双方向通信が必須で、プレイヤーの操作を即座にサーバーに送信し、他のプレイヤーの動きをリアルタイムで受信する必要がある[10]。

**3. コラボレーションツール**
Google DocsやFigmaのような共同編集ツールでは、各ユーザーの操作を即座に同期する必要がある[10]。

**4. IoT双方向制御**
センサーデータの受信だけでなく、デバイスへのコマンド送信も必要な場合[11]。

### SSEが優位なケース

以下のユースケースでは、SSEの採用が推奨される：

**1. 株価ティッカー・為替レート表示**
サーバーから一方向でデータをプッシュするだけで十分であり、SSEの自動再接続機能が有用[10]。

```javascript
// 株価ティッカーのSSE実装例
class StockTicker {
    constructor(symbols) {
        this.symbols = symbols;
        this.prices = new Map();
        this.eventSource = null;
        this.connect();
    }
    
    connect() {
        const params = new URLSearchParams({
            symbols: this.symbols.join(',')
        });
        
        this.eventSource = new EventSource(`/api/stocks?${params}`);
        
        this.eventSource.onmessage = (event) => {
            const data = JSON.parse(event.data);
            this.updatePrice(data.symbol, data.price, data.change);
        };
        
        // 自動再接続が標準で有効
        this.eventSource.onerror = (error) => {
            console.log('接続エラー、自動再接続を試行中...');
        };
    }
    
    updatePrice(symbol, price, change) {
        this.prices.set(symbol, { price, change });
        this.renderPriceUpdate(symbol);
    }
    
    renderPriceUpdate(symbol) {
        const { price, change } = this.prices.get(symbol);
        const element = document.getElementById(`stock-${symbol}`);
        element.innerHTML = `
            <span class="symbol">${symbol}</span>
            <span class="price">${price}</span>
            <span class="change ${change >= 0 ? 'positive' : 'negative'}">
                ${change >= 0 ? '+' : ''}${change}%
            </span>
        `;
    }
}
```

**2. 監視ダッシュボード**
Netflix HystrixやGrafanaのような監視システムでは、メトリクスデータの一方向配信で十分[11]。

**3. 通知システム**
プッシュ通知やアラートなど、サーバー起点のイベント配信[11]。

**4. ライブコメンタリー・実況**
スポーツ実況やイベント中継など、視聴者からの入力が不要な配信[11]。

### 判断フローチャート

```
┌─────────────────────────────────────────┐
│          技術選択フローチャート            │
└─────────────────────────────────────────┘
                    │
                    ▼
        ┌───────────────────────┐
        │ 双方向通信が必要か？     │
        └───────────────────────┘
                    │
        ┌──────────┴──────────┐
        │                      │
       YES                     NO
        │                      │
        ▼                      ▼
┌──────────────┐    ┌───────────────────┐
│バイナリデータ │    │ 自動再接続が      │
│送信が必要か？ │    │ 重要か？          │
└──────────────┘    └───────────────────┘
        │                      │
   ┌────┴────┐          ┌──────┴──────┐
  YES       NO         YES           NO
   │         │          │             │
   ▼         ▼          ▼             ▼
┌──────┐┌────────┐┌─────┐    ┌──────────┐
│      ││低遅延が ││     │    │実装の     │
│ WS   ││最重要？ ││ SSE │    │簡潔さ重視？│
│      │└────────┘│     │    └──────────┘
│推奨  │     │      │推奨 │          │
└──────┘   YES/NO   └─────┘     ┌────┴────┐
             │                   YES       NO
             ▼                    │         │
        ┌────────┐              ▼         ▼
        │  WS    │           ┌─────┐  ┌────┐
        │  推奨   │           │ SSE │  │ WS │
        └────────┘           │推奨 │  │推奨│
                             └─────┘  └────┘
```

## 実装における注意点とベストプラクティス

### セキュリティ対策（2024年最新）

**CSRF対策**
WebSocketでは、接続時の認証が重要となる。トークンベース認証（JWT）の使用が強く推奨される[12]。

```javascript
// JWTを使用したWebSocketセキュア接続
class SecureWebSocketClient {
    constructor(token) {
        this.token = token;
    }
    
    async connect() {
        // トークンをクエリパラメータまたはヘッダーで送信
        const ws = new WebSocket(`wss://api.example.com/ws?token=${this.token}`);
        
        ws.onopen = () => {
            // 接続確立後も定期的に認証状態を確認
            this.startHeartbeat(ws);
        };
        
        ws.onmessage = (event) => {
            const message = JSON.parse(event.data);
            
            // メッセージレベルでの検証
            if (!this.validateMessage(message)) {
                console.error('Invalid message received');
                return;
            }
            
            this.handleMessage(message);
        };
    }
    
    validateMessage(message) {
        // 入力検証とサニタイゼーション
        if (!message.type || !message.data) {
            return false;
        }
        
        // XSS対策：HTMLエスケープ
        if (typeof message.data === 'string') {
            message.data = this.escapeHtml(message.data);
        }
        
        return true;
    }
    
    escapeHtml(text) {
        const map = {
            '&': '&amp;',
            '<': '&lt;',
            '>': '&gt;',
            '"': '&quot;',
            "'": '&#39;'
        };
        return text.replace(/[&<>"']/g, m => map[m]);
    }
}
```

SSEの場合は、通常のHTTPセキュリティ対策が適用可能である：

```javascript
// SSEのセキュア実装（Express.js）
app.get('/events', authenticate, (req, res) => {
    // CORS設定
    res.setHeader('Access-Control-Allow-Origin', 'https://trusted-domain.com');
    res.setHeader('Access-Control-Allow-Credentials', 'true');
    
    // SSEヘッダー設定
    res.setHeader('Content-Type', 'text/event-stream');
    res.setHeader('Cache-Control', 'no-cache');
    res.setHeader('Connection', 'keep-alive');
    
    // X-Frame-Options でクリックジャッキング対策
    res.setHeader('X-Frame-Options', 'DENY');
    
    // Content-Security-Policy
    res.setHeader('Content-Security-Policy', "default-src 'self'");
    
    // データ送信時の検証
    const sendEvent = (data) => {
        // 入力検証
        if (!isValidData(data)) {
            return;
        }
        
        // JSONエンコード（自動エスケープ）
        res.write(`data: ${JSON.stringify(data)}\n\n`);
    };
});
```

### インフラ要件

**プロキシ設定**
WebSocketは特別な設定が必要な場合がある：

```nginx
# Nginx設定例
location /ws {
    proxy_pass http://backend;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    
    # タイムアウト設定
    proxy_read_timeout 86400;
    proxy_send_timeout 86400;
}
```

SSEの場合、標準的なHTTPプロキシ設定で動作するが、バッファリングを無効にする必要がある：

```nginx
# SSE用Nginx設定
location /events {
    proxy_pass http://backend;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    
    # SSE用の重要な設定
    proxy_set_header Connection '';
    proxy_http_version 1.1;
    chunked_transfer_encoding off;
    proxy_buffering off;
    proxy_cache off;
}
```

**ロードバランサー考慮**
WebSocketではsticky session（セッション維持）が推奨される[13]：

```yaml
# Kubernetes Ingress設定例
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: websocket-ingress
  annotations:
    nginx.ingress.kubernetes.io/affinity: "cookie"
    nginx.ingress.kubernetes.io/affinity-mode: "persistent"
    nginx.ingress.kubernetes.io/proxy-read-timeout: "3600"
    nginx.ingress.kubernetes.io/proxy-send-timeout: "3600"
spec:
  rules:
  - host: api.example.com
    http:
      paths:
      - path: /ws
        pathType: Prefix
        backend:
          service:
            name: websocket-service
            port:
              number: 8080
```

### 自動再接続とエラーハンドリング

SSEは自動再接続を標準でサポートしているが、WebSocketでは手動実装が必要：

```javascript
// WebSocket再接続ロジック実装
class ReconnectingWebSocket {
    constructor(url, options = {}) {
        this.url = url;
        this.reconnectInterval = options.reconnectInterval || 1000;
        this.maxReconnectInterval = options.maxReconnectInterval || 30000;
        this.reconnectDecay = options.reconnectDecay || 1.5;
        this.reconnectAttempts = 0;
        this.maxReconnectAttempts = options.maxReconnectAttempts || null;
        
        this.connect();
    }
    
    connect() {
        this.ws = new WebSocket(this.url);
        
        this.ws.onopen = () => {
            console.log('WebSocket接続確立');
            this.reconnectAttempts = 0;
        };
        
        this.ws.onclose = (event) => {
            console.log(`WebSocket切断: ${event.code}`);
            this.reconnect();
        };
        
        this.ws.onerror = (error) => {
            console.error('WebSocketエラー:', error);
        };
    }
    
    reconnect() {
        if (this.maxReconnectAttempts && 
            this.reconnectAttempts >= this.maxReconnectAttempts) {
            console.error('最大再接続試行回数に到達');
            return;
        }
        
        this.reconnectAttempts++;
        const timeout = Math.min(
            this.reconnectInterval * Math.pow(this.reconnectDecay, this.reconnectAttempts - 1),
            this.maxReconnectInterval
        );
        
        console.log(`${timeout}ms後に再接続を試行（試行回数: ${this.reconnectAttempts}）`);
        
        setTimeout(() => {
            console.log('再接続中...');
            this.connect();
        }, timeout);
    }
    
    send(data) {
        if (this.ws.readyState === WebSocket.OPEN) {
            this.ws.send(data);
        } else {
            console.warn('WebSocket未接続のため送信をキューに追加');
            // 実装によってはキューに追加して接続後に送信
        }
    }
}
```

## 実装コード例とデモ

### WebSocket実装例（Node.js + ws）

サーバー側実装：

```javascript
// server.js - WebSocketサーバー実装
const WebSocket = require('ws');
const http = require('http');
const express = require('express');
const jwt = require('jsonwebtoken');

const app = express();
const server = http.createServer(app);
const wss = new WebSocket.Server({ server });

// 接続管理
const clients = new Map();

// JWT認証ミドルウェア
const authenticateWebSocket = (ws, req) => {
    const token = new URL(req.url, `http://${req.headers.host}`).searchParams.get('token');
    
    try {
        const decoded = jwt.verify(token, process.env.JWT_SECRET);
        return decoded;
    } catch (err) {
        ws.close(1008, 'Invalid token');
        return null;
    }
};

wss.on('connection', (ws, req) => {
    // 認証
    const user = authenticateWebSocket(ws, req);
    if (!user) return;
    
    // クライアント登録
    const clientId = generateClientId();
    clients.set(clientId, {
        ws,
        user,
        lastActivity: Date.now()
    });
    
    console.log(`Client ${clientId} connected (User: ${user.username})`);
    
    // Welcome メッセージ送信
    ws.send(JSON.stringify({
        type: 'welcome',
        clientId,
        message: 'Connected to WebSocket server'
    }));
    
    // メッセージ処理
    ws.on('message', (message) => {
        try {
            const data = JSON.parse(message);
            handleMessage(clientId, data);
        } catch (err) {
            console.error('Invalid message format:', err);
            ws.send(JSON.stringify({
                type: 'error',
                message: 'Invalid message format'
            }));
        }
    });
    
    // 切断処理
    ws.on('close', () => {
        console.log(`Client ${clientId} disconnected`);
        clients.delete(clientId);
        broadcastUserList();
    });
    
    // エラー処理
    ws.on('error', (error) => {
        console.error(`Client ${clientId} error:`, error);
    });
    
    // 初期データ送信
    sendInitialData(ws);
    broadcastUserList();
});

// メッセージハンドラー
function handleMessage(clientId, data) {
    const client = clients.get(clientId);
    if (!client) return;
    
    client.lastActivity = Date.now();
    
    switch (data.type) {
        case 'chat':
            broadcastMessage({
                type: 'chat',
                user: client.user.username,
                message: data.message,
                timestamp: Date.now()
            });
            break;
            
        case 'ping':
            client.ws.send(JSON.stringify({
                type: 'pong',
                timestamp: Date.now()
            }));
            break;
            
        case 'subscribe':
            handleSubscription(clientId, data.channel);
            break;
            
        default:
            console.warn(`Unknown message type: ${data.type}`);
    }
}

// ブロードキャスト関数
function broadcastMessage(message) {
    const messageStr = JSON.stringify(message);
    
    clients.forEach((client) => {
        if (client.ws.readyState === WebSocket.OPEN) {
            client.ws.send(messageStr);
        }
    });
}

// ユーザーリスト更新
function broadcastUserList() {
    const users = Array.from(clients.values()).map(c => ({
        username: c.user.username,
        lastActivity: c.lastActivity
    }));
    
    broadcastMessage({
        type: 'userList',
        users
    });
}

// 定期的なヘルスチェック
setInterval(() => {
    clients.forEach((client, clientId) => {
        if (client.ws.readyState === WebSocket.OPEN) {
            client.ws.ping();
        } else {
            clients.delete(clientId);
        }
    });
}, 30000);

server.listen(8080, () => {
    console.log('WebSocket server listening on port 8080');
});
```

クライアント側実装：

```javascript
// client.js - WebSocketクライアント実装
class WebSocketClient {
    constructor(url, token) {
        this.url = url;
        this.token = token;
        this.ws = null;
        this.messageHandlers = new Map();
        this.isConnected = false;
        this.reconnectTimer = null;
        this.messageQueue = [];
    }
    
    connect() {
        return new Promise((resolve, reject) => {
            try {
                this.ws = new WebSocket(`${this.url}?token=${this.token}`);
                
                this.ws.onopen = () => {
                    console.log('WebSocket connected');
                    this.isConnected = true;
                    this.flushMessageQueue();
                    resolve();
                };
                
                this.ws.onmessage = (event) => {
                    this.handleMessage(event.data);
                };
                
                this.ws.onerror = (error) => {
                    console.error('WebSocket error:', error);
                    reject(error);
                };
                
                this.ws.onclose = (event) => {
                    console.log('WebSocket disconnected:', event.code, event.reason);
                    this.isConnected = false;
                    this.scheduleReconnect();
                };
                
            } catch (error) {
                reject(error);
            }
        });
    }
    
    handleMessage(data) {
        try {
            const message = JSON.parse(data);
            console.log('Received:', message);
            
            // タイプ別ハンドラー呼び出し
            const handler = this.messageHandlers.get(message.type);
            if (handler) {
                handler(message);
            }
            
            // 共通処理
            this.updateUI(message);
            
        } catch (error) {
            console.error('Failed to parse message:', error);
        }
    }
    
    on(type, handler) {
        this.messageHandlers.set(type, handler);
    }
    
    send(type, data) {
        const message = {
            type,
            ...data,
            timestamp: Date.now()
        };
        
        if (this.isConnected && this.ws.readyState === WebSocket.OPEN) {
            this.ws.send(JSON.stringify(message));
        } else {
            console.log('Queueing message:', message);
            this.messageQueue.push(message);
        }
    }
    
    flushMessageQueue() {
        while (this.messageQueue.length > 0) {
            const message = this.messageQueue.shift();
            this.ws.send(JSON.stringify(message));
        }
    }
    
    scheduleReconnect() {
        if (this.reconnectTimer) {
            clearTimeout(this.reconnectTimer);
        }
        
        this.reconnectTimer = setTimeout(() => {
            console.log('Attempting to reconnect...');
            this.connect();
        }, 3000);
    }
    
    updateUI(message) {
        // UI更新ロジック
        switch(message.type) {
            case 'chat':
                this.addChatMessage(message);
                break;
            case 'userList':
                this.updateUserList(message.users);
                break;
            case 'notification':
                this.showNotification(message);
                break;
        }
    }
    
    addChatMessage(message) {
        const chatContainer = document.getElementById('chat-messages');
        const messageEl = document.createElement('div');
        messageEl.className = 'chat-message';
        messageEl.innerHTML = `
            <span class="user">${this.escapeHtml(message.user)}:</span>
            <span class="text">${this.escapeHtml(message.message)}</span>
            <span class="time">${new Date(message.timestamp).toLocaleTimeString()}</span>
        `;
        chatContainer.appendChild(messageEl);
        chatContainer.scrollTop = chatContainer.scrollHeight;
    }
    
    escapeHtml(text) {
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
    }
    
    disconnect() {
        if (this.reconnectTimer) {
            clearTimeout(this.reconnectTimer);
            this.reconnectTimer = null;
        }
        
        if (this.ws) {
            this.ws.close();
            this.ws = null;
        }
        
        this.isConnected = false;
    }
}

// 使用例
const client = new WebSocketClient('ws://localhost:8080', 'your-jwt-token');

// メッセージハンドラー登録
client.on('welcome', (message) => {
    console.log('Welcome message:', message);
});

client.on('chat', (message) => {
    console.log('Chat message:', message);
});

// 接続
client.connect().then(() => {
    // チャットメッセージ送信
    client.send('chat', {
        message: 'Hello, everyone!'
    });
});
```

### SSE実装例（Express + EventSource）

サーバー側実装：

```javascript
// sse-server.js - SSEサーバー実装
const express = require('express');
const cors = require('cors');

const app = express();

// CORS設定
app.use(cors({
    origin: 'http://localhost:3000',
    credentials: true
}));

// SSEクライアント管理
const sseClients = new Map();
let clientIdCounter = 0;

// SSEエンドポイント
app.get('/events', (req, res) => {
    // SSEヘッダー設定
    res.setHeader('Content-Type', 'text/event-stream');
    res.setHeader('Cache-Control', 'no-cache');
    res.setHeader('Connection', 'keep-alive');
    res.setHeader('X-Accel-Buffering', 'no'); // Nginx用
    
    // クライアントID生成
    const clientId = ++clientIdCounter;
    
    // クライアント登録
    const client = {
        id: clientId,
        res,
        subscriptions: new Set(['default'])
    };
    sseClients.set(clientId, client);
    
    console.log(`SSE client ${clientId} connected`);
    
    // 初期メッセージ送信
    sendSSEMessage(res, {
        type: 'connected',
        clientId,
        message: 'SSE connection established'
    });
    
    // 定期的なハートビート
    const heartbeatInterval = setInterval(() => {
        sendSSEMessage(res, { type: 'heartbeat', timestamp: Date.now() });
    }, 30000);
    
    // クライアント切断処理
    req.on('close', () => {
        console.log(`SSE client ${clientId} disconnected`);
        clearInterval(heartbeatInterval);
        sseClients.delete(clientId);
    });
});

// SSEメッセージ送信関数
function sendSSEMessage(res, data, event = null, id = null) {
    let message = '';
    
    if (id) {
        message += `id: ${id}\n`;
    }
    
    if (event) {
        message += `event: ${event}\n`;
    }
    
    message += `data: ${JSON.stringify(data)}\n\n`;
    
    res.write(message);
}

// ブロードキャスト関数
function broadcastToChannel(channel, data, event = null) {
    sseClients.forEach((client) => {
        if (client.subscriptions.has(channel)) {
            sendSSEMessage(client.res, data, event);
        }
    });
}

// 株価データシミュレーション
const stockSymbols = ['AAPL', 'GOOGL', 'MSFT', 'AMZN', 'TSLA'];
const stockPrices = new Map();

// 初期価格設定
stockSymbols.forEach(symbol => {
    stockPrices.set(symbol, {
        price: 100 + Math.random() * 400,
        change: 0
    });
});

// 株価更新シミュレーション
setInterval(() => {
    stockSymbols.forEach(symbol => {
        const current = stockPrices.get(symbol);
        const changePercent = (Math.random() - 0.5) * 2; // -1% to +1%
        const newPrice = current.price * (1 + changePercent / 100);
        
        stockPrices.set(symbol, {
            price: newPrice,
            change: changePercent
        });
        
        // 株価更新をブロードキャスト
        broadcastToChannel('stocks', {
            symbol,
            price: newPrice.toFixed(2),
            change: changePercent.toFixed(2),
            timestamp: Date.now()
        }, 'stock-update');
    });
}, 2000);

// システム通知エンドポイント
app.post('/notify', express.json(), (req, res) => {
    const { message, level = 'info', channel = 'default' } = req.body;
    
    broadcastToChannel(channel, {
        message,
        level,
        timestamp: Date.now()
    }, 'notification');
    
    res.json({ success: true, clientsNotified: sseClients.size });
});

// メトリクスデータ生成
let cpuUsage = 50;
let memoryUsage = 60;

setInterval(() => {
    // メトリクスのシミュレーション
    cpuUsage = Math.max(0, Math.min(100, cpuUsage + (Math.random() - 0.5) * 10));
    memoryUsage = Math.max(0, Math.min(100, memoryUsage + (Math.random() - 0.5) * 5));
    
    broadcastToChannel('metrics', {
        cpu: cpuUsage.toFixed(1),
        memory: memoryUsage.toFixed(1),
        connections: sseClients.size,
        timestamp: Date.now()
    }, 'metrics-update');
}, 1000);

app.listen(8081, () => {
    console.log('SSE server listening on port 8081');
});
```

クライアント側実装：

```javascript
// sse-client.js - SSEクライアント実装
class SSEClient {
    constructor(url) {
        this.url = url;
        this.eventSource = null;
        this.handlers = new Map();
        this.reconnectAttempts = 0;
        this.maxReconnectAttempts = 10;
    }
    
    connect() {
        console.log('Connecting to SSE server...');
        this.eventSource = new EventSource(this.url);
        
        // 標準イベントハンドラー
        this.eventSource.onopen = () => {
            console.log('SSE connection opened');
            this.reconnectAttempts = 0;
            this.onConnected();
        };
        
        this.eventSource.onerror = (error) => {
            console.error('SSE error:', error);
            
            if (this.eventSource.readyState === EventSource.CLOSED) {
                console.log('SSE connection closed');
                this.handleReconnection();
            }
        };
        
        // デフォルトメッセージハンドラー
        this.eventSource.onmessage = (event) => {
            this.handleMessage(JSON.parse(event.data));
        };
        
        // カスタムイベントハンドラー登録
        this.registerEventHandlers();
    }
    
    registerEventHandlers() {
        // 株価更新イベント
        this.eventSource.addEventListener('stock-update', (event) => {
            const data = JSON.parse(event.data);
            this.handleStockUpdate(data);
        });
        
        // 通知イベント
        this.eventSource.addEventListener('notification', (event) => {
            const data = JSON.parse(event.data);
            this.handleNotification(data);
        });
        
        // メトリクス更新イベント
        this.eventSource.addEventListener('metrics-update', (event) => {
            const data = JSON.parse(event.data);
            this.handleMetricsUpdate(data);
        });
    }
    
    handleMessage(data) {
        console.log('Received message:', data);
        
        // タイプ別処理
        const handler = this.handlers.get(data.type);
        if (handler) {
            handler(data);
        }
    }
    
    handleStockUpdate(data) {
        const stockElement = document.getElementById(`stock-${data.symbol}`);
        if (stockElement) {
            const changeClass = parseFloat(data.change) >= 0 ? 'positive' : 'negative';
            stockElement.innerHTML = `
                <div class="stock-item">
                    <span class="symbol">${data.symbol}</span>
                    <span class="price">$${data.price}</span>
                    <span class="change ${changeClass}">${data.change}%</span>
                </div>
            `;
            
            // アニメーション効果
            stockElement.classList.add('updated');
            setTimeout(() => stockElement.classList.remove('updated'), 500);
        }
    }
    
    handleNotification(data) {
        console.log('Notification:', data);
        
        // 通知UI表示
        const notificationContainer = document.getElementById('notifications');
        const notification = document.createElement('div');
        notification.className = `notification ${data.level}`;
        notification.innerHTML = `
            <div class="notification-content">
                <span class="message">${data.message}</span>
                <span class="time">${new Date(data.timestamp).toLocaleTimeString()}</span>
            </div>
        `;
        
        notificationContainer.insertBefore(notification, notificationContainer.firstChild);
        
        // 5秒後に自動削除
        setTimeout(() => {
            notification.classList.add('fade-out');
            setTimeout(() => notification.remove(), 300);
        }, 5000);
    }
    
    handleMetricsUpdate(data) {
        // メトリクス表示更新
        document.getElementById('cpu-usage').textContent = `${data.cpu}%`;
        document.getElementById('memory-usage').textContent = `${data.memory}%`;
        document.getElementById('connections').textContent = data.connections;
        
        // プログレスバー更新
        document.getElementById('cpu-bar').style.width = `${data.cpu}%`;
        document.getElementById('memory-bar').style.width = `${data.memory}%`;
    }
    
    on(type, handler) {
        this.handlers.set(type, handler);
    }
    
    handleReconnection() {
        if (this.reconnectAttempts >= this.maxReconnectAttempts) {
            console.error('Max reconnection attempts reached');
            this.onMaxReconnectAttemptsReached();
            return;
        }
        
        this.reconnectAttempts++;
        const delay = Math.min(1000 * Math.pow(2, this.reconnectAttempts - 1), 30000);
        
        console.log(`Reconnecting in ${delay}ms (attempt ${this.reconnectAttempts})`);
        
        setTimeout(() => {
            this.disconnect();
            this.connect();
        }, delay);
    }
    
    onConnected() {
        // UI更新など
        document.getElementById('connection-status').textContent = 'Connected';
        document.getElementById('connection-status').className = 'connected';
    }
    
    onMaxReconnectAttemptsReached() {
        document.getElementById('connection-status').textContent = 'Disconnected';
        document.getElementById('connection-status').className = 'disconnected';
    }
    
    disconnect() {
        if (this.eventSource) {
            this.eventSource.close();
            this.eventSource = null;
        }
    }
}

// 使用例
const sseClient = new SSEClient('http://localhost:8081/events');

// カスタムハンドラー登録
sseClient.on('connected', (data) => {
    console.log('Connected with client ID:', data.clientId);
});

sseClient.on('heartbeat', (data) => {
    console.log('Heartbeat received:', new Date(data.timestamp));
});

// 接続開始
sseClient.connect();

// UIの初期化
document.addEventListener('DOMContentLoaded', () => {
    // 株価表示エリア作成
    const stockContainer = document.getElementById('stocks');
    ['AAPL', 'GOOGL', 'MSFT', 'AMZN', 'TSLA'].forEach(symbol => {
        const div = document.createElement('div');
        div.id = `stock-${symbol}`;
        div.className = 'stock-container';
        stockContainer.appendChild(div);
    });
});
```

### 比較デモの構築

両技術の性能を比較するデモアプリケーション：

```html
<!-- comparison-demo.html -->
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WebSocket vs SSE Performance Comparison</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 20px;
            background: #f5f5f5;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .comparison-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 20px;
        }
        
        .tech-panel {
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .tech-panel h2 {
            margin-top: 0;
            color: #333;
        }
        
        .metrics {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin: 20px 0;
        }
        
        .metric {
            padding: 10px;
            background: #f8f9fa;
            border-radius: 4px;
        }
        
        .metric-label {
            font-size: 12px;
            color: #666;
        }
        
        .metric-value {
            font-size: 24px;
            font-weight: bold;
            color: #333;
        }
        
        .status {
            padding: 5px 10px;
            border-radius: 4px;
            display: inline-block;
            font-size: 12px;
            font-weight: bold;
        }
        
        .status.connected {
            background: #d4edda;
            color: #155724;
        }
        
        .status.disconnected {
            background: #f8d7da;
            color: #721c24;
        }
        
        .message-log {
            height: 200px;
            overflow-y: auto;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 10px;
            font-family: monospace;
            font-size: 12px;
            background: #f8f9fa;
        }
        
        .controls {
            margin: 20px 0;
        }
        
        button {
            padding: 8px 16px;
            margin-right: 10px;
            border: none;
            border-radius: 4px;
            background: #007bff;
            color: white;
            cursor: pointer;
        }
        
        button:hover {
            background: #0056b3;
        }
        
        button:disabled {
            background: #ccc;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>WebSocket vs SSE パフォーマンス比較デモ</h1>
        
        <div class="comparison-grid">
            <!-- WebSocketパネル -->
            <div class="tech-panel">
                <h2>WebSocket</h2>
                <div class="status" id="ws-status">未接続</div>
                
                <div class="metrics">
                    <div class="metric">
                        <div class="metric-label">レイテンシ</div>
                        <div class="metric-value" id="ws-latency">-</div>
                    </div>
                    <div class="metric">
                        <div class="metric-label">メッセージ/秒</div>
                        <div class="metric-value" id="ws-throughput">0</div>
                    </div>
                    <div class="metric">
                        <div class="metric-label">受信総数</div>
                        <div class="metric-value" id="ws-total">0</div>
                    </div>
                    <div class="metric">
                        <div class="metric-label">エラー数</div>
                        <div class="metric-value" id="ws-errors">0</div>
                    </div>
                </div>
                
                <div class="controls">
                    <button id="ws-connect">接続</button>
                    <button id="ws-disconnect">切断</button>
                    <button id="ws-send">メッセージ送信</button>
                    <button id="ws-benchmark">ベンチマーク開始</button>
                </div>
                
                <div class="message-log" id="ws-log"></div>
            </div>
            
            <!-- SSEパネル -->
            <div class="tech-panel">
                <h2>Server-Sent Events</h2>
                <div class="status" id="sse-status">未接続</div>
                
                <div class="metrics">
                    <div class="metric">
                        <div class="metric-label">レイテンシ</div>
                        <div class="metric-value" id="sse-latency">-</div>
                    </div>
                    <div class="metric">
                        <div class="metric-label">メッセージ/秒</div>
                        <div class="metric-value" id="sse-throughput">0</div>
                    </div>
                    <div class="metric">
                        <div class="metric-label">受信総数</div>
                        <div class="metric-value" id="sse-total">0</div>
                    </div>
                    <div class="metric">
                        <div class="metric-label">再接続数</div>
                        <div class="metric-value" id="sse-reconnects">0</div>
                    </div>
                </div>
                
                <div class="controls">
                    <button id="sse-connect">接続</button>
                    <button id="sse-disconnect">切断</button>
                    <button id="sse-subscribe">購読開始</button>
                    <button id="sse-benchmark">ベンチマーク開始</button>
                </div>
                
                <div class="message-log" id="sse-log"></div>
            </div>
        </div>
        
        <div style="margin-top: 40px;">
            <h2>比較結果</h2>
            <canvas id="comparison-chart" width="800" height="400"></canvas>
        </div>
    </div>
    
    <script>
        // WebSocket比較実装
        class WebSocketBenchmark {
            constructor() {
                this.ws = null;
                this.metrics = {
                    total: 0,
                    errors: 0,
                    latencies: [],
                    startTime: null,
                    messageTimestamps: []
                };
            }
            
            connect() {
                this.ws = new WebSocket('ws://localhost:8080');
                
                this.ws.onopen = () => {
                    document.getElementById('ws-status').textContent = '接続済み';
                    document.getElementById('ws-status').className = 'status connected';
                    this.log('Connected to WebSocket server');
                };
                
                this.ws.onmessage = (event) => {
                    this.metrics.total++;
                    this.metrics.messageTimestamps.push(Date.now());
                    
                    try {
                        const data = JSON.parse(event.data);
                        if (data.type === 'pong') {
                            const latency = Date.now() - data.clientTimestamp;
                            this.metrics.latencies.push(latency);
                            this.updateLatency(latency);
                        }
                        this.log(`Received: ${data.type}`);
                    } catch (err) {
                        this.metrics.errors++;
                    }
                    
                    this.updateMetrics();
                };
                
                this.ws.onerror = (error) => {
                    this.metrics.errors++;
                    this.log(`Error: ${error.type}`);
                };
                
                this.ws.onclose = () => {
                    document.getElementById('ws-status').textContent = '切断';
                    document.getElementById('ws-status').className = 'status disconnected';
                    this.log('Disconnected');
                };
            }
            
            disconnect() {
                if (this.ws) {
                    this.ws.close();
                }
            }
            
            sendMessage() {
                if (this.ws && this.ws.readyState === WebSocket.OPEN) {
                    this.ws.send(JSON.stringify({
                        type: 'ping',
                        clientTimestamp: Date.now()
                    }));
                }
            }
            
            startBenchmark() {
                this.metrics.startTime = Date.now();
                this.metrics.messageTimestamps = [];
                
                // 高頻度メッセージ送信
                const interval = setInterval(() => {
                    if (this.ws && this.ws.readyState === WebSocket.OPEN) {
                        this.sendMessage();
                    } else {
                        clearInterval(interval);
                    }
                }, 100);
                
                // 10秒後に停止
                setTimeout(() => {
                    clearInterval(interval);
                    this.log('Benchmark completed');
                }, 10000);
            }
            
            updateMetrics() {
                document.getElementById('ws-total').textContent = this.metrics.total;
                document.getElementById('ws-errors').textContent = this.metrics.errors;
                
                // スループット計算
                const now = Date.now();
                const recentMessages = this.metrics.messageTimestamps.filter(
                    t => now - t < 1000
                );
                document.getElementById('ws-throughput').textContent = recentMessages.length;
            }
            
            updateLatency(latency) {
                document.getElementById('ws-latency').textContent = `${latency}ms`;
            }
            
            log(message) {
                const logEl = document.getElementById('ws-log');
                const timestamp = new Date().toLocaleTimeString();
                logEl.innerHTML += `[${timestamp}] ${message}\n`;
                logEl.scrollTop = logEl.scrollHeight;
            }
        }
        
        // SSE比較実装
        class SSEBenchmark {
            constructor() {
                this.eventSource = null;
                this.metrics = {
                    total: 0,
                    reconnects: 0,
                    latencies: [],
                    startTime: null,
                    messageTimestamps: []
                };
            }
            
            connect() {
                this.eventSource = new EventSource('http://localhost:8081/events');
                
                this.eventSource.onopen = () => {
                    document.getElementById('sse-status').textContent = '接続済み';
                    document.getElementById('sse-status').className = 'status connected';
                    this.log('Connected to SSE server');
                };
                
                this.eventSource.onmessage = (event) => {
                    this.metrics.total++;
                    this.metrics.messageTimestamps.push(Date.now());
                    
                    try {
                        const data = JSON.parse(event.data);
                        if (data.timestamp) {
                            const latency = Date.now() - data.timestamp;
                            this.metrics.latencies.push(latency);
                            this.updateLatency(latency);
                        }
                        this.log(`Received: ${data.type || 'message'}`);
                    } catch (err) {
                        // エラー処理
                    }
                    
                    this.updateMetrics();
                };
                
                this.eventSource.onerror = () => {
                    if (this.eventSource.readyState === EventSource.CLOSED) {
                        document.getElementById('sse-status').textContent = '切断';
                        document.getElementById('sse-status').className = 'status disconnected';
                    } else {
                        this.metrics.reconnects++;
                        this.log('Reconnecting...');
                    }
                };
            }
            
            disconnect() {
                if (this.eventSource) {
                    this.eventSource.close();
                }
            }
            
            updateMetrics() {
                document.getElementById('sse-total').textContent = this.metrics.total;
                document.getElementById('sse-reconnects').textContent = this.metrics.reconnects;
                
                // スループット計算
                const now = Date.now();
                const recentMessages = this.metrics.messageTimestamps.filter(
                    t => now - t < 1000
                );
                document.getElementById('sse-throughput').textContent = recentMessages.length;
            }
            
            updateLatency(latency) {
                document.getElementById('sse-latency').textContent = `${latency}ms`;
            }
            
            log(message) {
                const logEl = document.getElementById('sse-log');
                const timestamp = new Date().toLocaleTimeString();
                logEl.innerHTML += `[${timestamp}] ${message}\n`;
                logEl.scrollTop = logEl.scrollHeight;
            }
        }
        
        // 初期化
        const wsBenchmark = new WebSocketBenchmark();
        const sseBenchmark = new SSEBenchmark();
        
        // イベントハンドラー設定
        document.getElementById('ws-connect').onclick = () => wsBenchmark.connect();
        document.getElementById('ws-disconnect').onclick = () => wsBenchmark.disconnect();
        document.getElementById('ws-send').onclick = () => wsBenchmark.sendMessage();
        document.getElementById('ws-benchmark').onclick = () => wsBenchmark.startBenchmark();
        
        document.getElementById('sse-connect').onclick = () => sseBenchmark.connect();
        document.getElementById('sse-disconnect').onclick = () => sseBenchmark.disconnect();
    </script>
</body>
</html>
```

## まとめ：2025年の技術選択指針

2025年のリアルタイム通信技術選択において、「とりあえずWebSocket」という安易な判断から脱却し、要件に基づいた適切な選択を行うことが重要である。HTTP/2の普及により、SSEは従来の6接続制限を克服し、多くのユースケースで実用的な選択肢となった。

技術選択の決定木をまとめると、双方向通信やバイナリデータ送信が必要な場合はWebSocket一択だが、サーバーからクライアントへの単方向通信で十分な場合は、SSEのシンプルさと自動再接続機能が大きなメリットとなる。パフォーマンス面では両技術とも300万イベント/秒という驚異的なスループットを実現可能で、実用上の差はCPU効率のわずかな違いに留まる。

今後はWebTransportなど新技術の登場により選択肢がさらに広がることが予想される。技術者として重要なのは、各技術の特性を正確に理解し、プロジェクトの要件に最適な選択を行う判断力を養うことである。本記事で提供した判断フローチャートと実装例を活用し、自信を持って技術選択を行っていただきたい。

**表3: 技術選択クイックリファレンス**

| 要件 | 推奨技術 | 理由 |
|------|----------|------|
| チャット・コラボレーション | WebSocket | 双方向通信必須 |
| 株価・ニュース配信 | SSE | 単方向で十分、自動再接続 |
| オンラインゲーム | WebSocket | 低レイテンシ双方向通信 |
| 監視ダッシュボード | SSE | サーバープッシュのみで十分 |
| ファイル転送 | WebSocket | バイナリデータサポート |
| 通知システム | SSE | シンプルな実装で十分 |
| IoT双方向制御 | WebSocket | デバイス制御が必要 |
| ライブストリーミング | SSE/WebSocket | 要件による |

## 参考文献

[1] RFC 6455 - The WebSocket Protocol, IETF, 2011  
[2] WebSocket Protocol Registries, IANA, 2024  
[3] Server-sent events, W3C/WHATWG Living Standard, 2024  
[4] EventSource API Specification, W3C, 2024  
[5] RFC 7540 - Hypertext Transfer Protocol Version 2 (HTTP/2), IETF, 2015  
[6] HTTP/2 Multiplexing and Connection Limits, Mozilla Developer Network, 2024  
[7] Browser Support Statistics, Can I Use, 2025  
[8] WebSocket vs SSE Performance Comparison, Timeplus, 2024  
[9] Real-time Communication Latency Measurements, Ably, 2024  
[10] WebSocket Use Cases and Best Practices, freeCodeCamp, 2024  
[11] SSE Implementation Patterns, dev.to, 2024  
[12] WebSocket Security Guidelines, OWASP, 2024  
[13] Load Balancing WebSocket Connections, NGINX Documentation, 2024