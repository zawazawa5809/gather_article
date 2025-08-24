---
permalink: /electron-vs-tauri-2025-complete-guide
title: "【2025年最新】Electron vs Tauri 個人開発の完璧な選択ガイド"
summary: "個人開発者向けにElectronとTauriを徹底比較。パフォーマンス90%改善の真実、実装事例、2025年の選択基準を解説。ベンチマーク付き15,000字の完全ガイド。"
tags:
  - "#desktop-development"
  - "#electron"
  - "#tauri"
  - "#rust"
  - "#javascript"
  - "#performance-optimization"
  - "#2025-trends"
  - "#individual-development"
  - "#cross-platform"
  - "#framework-comparison"
---

# 【2025年最新】Electron vs Tauri 個人開発の完璧な選択ガイド - パフォーマンス90%削減の真実とは

## はじめに：なぜ今、フレームワーク選択が重要なのか

2025年、個人開発者やフリーランスがデスクトップアプリケーションを開発する際、最も重要な決断の一つが**フレームワーク選択**です。かつてElectron一強だったこの分野に、Tauriという革新的な選択肢が登場し、**メモリ使用量50%削減**、**バンドルサイズ90%削減**という驚異的なパフォーマンス改善を実現しています[1]。

しかし、数値だけで判断するのは危険です。個人開発者が直面する現実的な課題として、**学習コスト**、**開発速度**、**エコシステムの充実度**、そして**将来的な保守性**があります。本記事では、2024-2025年の最新動向を踏まえ、15,000字にわたって両フレームワークを徹底比較し、あなたのプロジェクトに最適な選択を導き出します。

本記事を読むことで、**技術選定の迷いを解消**し、**開発時間を大幅に短縮**できる実践的な知識を得られます。さらに、実際の開発者の成功事例と失敗談から、**リスクを最小化する具体的な戦略**も学べます。

## 30秒で理解！Electron vs Tauri クイック比較表

まず、両フレームワークの違いを一目で理解できる比較表をご覧ください。

### パフォーマンス比較表

| 項目 | Electron | Tauri | 差異 |
|------|----------|--------|------|
| **メモリ使用量** | 60-80MB以上 | 30-40MB | **50%削減**[1] |
| **バンドルサイズ** | 85-120MB | 2.5-10MB | **90%削減**[1][2] |
| **起動時間** | 1-2秒 | 500ms未満 | **75%高速化**[1] |
| **最小バイナリ** | 50MB以上 | 600KB未満 | **98%削減**[3] |

### 主要な技術的違い

| 特徴 | Electron | Tauri |
|------|----------|--------|
| **レンダリングエンジン** | Chromium（バンドル） | OS標準WebView |
| **バックエンド言語** | JavaScript/Node.js | Rust |
| **セキュリティモデル** | Node.js APIフルアクセス | サンドボックス化・最小権限 |
| **クロスプラットフォーム** | デスクトップのみ | デスクトップ＋モバイル（2.0以降） |
| **開発者体験** | JavaScript完結 | Rust＋フロントエンド |

### 選択フローチャート

```
スタート
│
├─ 新規プロジェクト？
│  │
│  ├─ Yes → パフォーマンス重視？
│  │         │
│  │         ├─ Yes → モバイル展開予定？
│  │         │         │
│  │         │         ├─ Yes → 【Tauri推奨】
│  │         │         └─ No → Rust学習可能？
│  │         │                  │
│  │         │                  ├─ Yes → 【Tauri推奨】
│  │         │                  └─ No → 【要検討】
│  │         │
│  │         └─ No → 豊富なnpmライブラリ必要？
│  │                   │
│  │                   ├─ Yes → 【Electron推奨】
│  │                   └─ No → 【Tauri検討】
│  │
│  └─ No（既存プロジェクト） → Electronベース？
│                               │
│                               ├─ Yes → 【Electron継続】
│                               └─ No → 【移行コスト評価】
```

## パフォーマンス徹底比較：数値で見る真実

### メモリ使用量の実測値

2024年のChadura氏によるベンチマーク[1]では、同一機能を持つアプリケーションで以下の結果が得られました：

**macOSでの測定結果：**
- **Electron**: Chromiumベースのレンダラープロセスが平均**78MB**のメモリを消費
- **Tauri**: WKWebViewプロセスが平均**36MB**のメモリを消費
- **削減率**: 約**54%のメモリ削減**を実現

この差は、ElectronがChromium全体をバンドルする一方、TauriがOSネイティブのWebView（軽量な描画エンジン）を利用することに起因します。特に、複数ウィンドウを開く場合、この差はさらに顕著になります。

**実アプリケーションでの比較（Levminer氏の事例）[2]：**

Levminer氏は同じ機能を持つ実アプリケーションを両フレームワークで実装し、以下の結果を報告しています：

```
初期起動時のメモリ使用量：
- Electron版: 165MB（メインプロセス45MB + レンダラー120MB）
- Tauri版: 42MB（Rustバックエンド12MB + WebView30MB）

1時間稼働後：
- Electron版: 210MB（ガベージコレクション後）
- Tauri版: 48MB（ほぼ変化なし）
```

### バンドルサイズ：90%削減の内訳

バンドルサイズの劇的な差は、アーキテクチャの根本的な違いから生まれます：

**Electronのバンドル構成（85-120MB）：**
1. **Chromiumブラウザエンジン**: 約60MB
2. **Node.jsランタイム**: 約15MB
3. **Electronフレームワーク**: 約10MB
4. **アプリケーションコード**: 数MB

**Tauriのバンドル構成（2.5-10MB）：**
1. **Rustバイナリ（最適化済み）**: 1-3MB
2. **フロントエンドアセット**: 1-5MB
3. **アイコン・リソース**: 数百KB

この差は配布時に大きな影響を与えます。特に：
- **ダウンロード時間**: 100Mbps回線でElectronアプリは7-10秒、Tauriアプリは0.2-1秒
- **ストレージ影響**: 10個のElectronアプリで1GB、同数のTauriアプリで50MB
- **自動更新**: 差分更新でもElectronは10-20MB、Tauriは1-2MB

### 起動時間とレスポンス性能

起動時間の測定結果（2024年ベンチマーク）[1]：

**コールドスタート（初回起動）：**
- **Electron**: 平均1,500ms（Chromium初期化に大半を消費）
- **Tauri**: 平均400ms（Rust起動は100ms、WebView初期化300ms）

**ホットスタート（2回目以降）：**
- **Electron**: 平均800ms（キャッシュ利用）
- **Tauri**: 平均250ms（OSレベルでWebViewがキャッシュ）

**レスポンス性能（IPC通信）：**

Tauri 2.0では、IPCレイヤーが完全に書き直され、Raw Payloads機能が追加されました[3]。これにより：

```javascript
// Electron - JSON serialization overhead
const largeData = await ipcRenderer.invoke('get-large-data');
// 10MBのデータ転送: 約150ms

// Tauri 2.0 - Raw Payloads
const largeData = await invoke('get_large_data');
// 10MBのデータ転送: 約30ms（5倍高速）
```

## 最新バージョンの機能比較（2024-2025）

### Tauri 2.0の革新的機能

2024年10月にリリースされたTauri 2.0[3][5]は、「The Mobile Update」と呼ばれ、以下の革新的機能を搭載しました：

**1. クロスプラットフォーム対応の拡大**
- **iOS/Android正式サポート**: 単一コードベースでデスクトップとモバイルの両方に対応
- **ネイティブコード統合**: SwiftやKotlinを直接呼び出し可能

```rust
// Tauri 2.0 - モバイル対応コマンド
#[tauri::command]
#[cfg(mobile)]
async fn mobile_specific_feature() -> Result<String, String> {
    // iOS/Android専用処理
    Ok("Mobile feature executed".to_string())
}
```

**2. プラグインシステムの強化**

公式プラグインが大幅に拡充され、以下が利用可能になりました[6]：

- **生体認証**: Touch ID/Face ID対応
- **NFC読み取り**: モバイルでのNFCタグ操作
- **SQLデータベース**: ローカルDB統合
- **プッシュ通知**: ネイティブ通知システム
- **カメラ/QRコード**: バーコードスキャン機能

**3. パフォーマンス最適化**

- **最小バイナリサイズ600KB未満**を実現[3]
- **Raw Payloads**: 大容量データ転送が5倍高速化
- **起動時間**: 500ms未満を安定的に達成

### Electron 34の進化

2024年12月リリースのElectron 34.0.0[4]も着実な進化を遂げています：

**1. 最新技術スタックへの対応**
- **Chromium 132**: 最新のWeb標準をフルサポート
- **V8 13.2**: JavaScript実行速度が15%向上
- **Node.js 20.18.1**: 安定版のLTSサポート

**2. Node.js 22への移行準備（2025年1-2月）**[4][7]

```javascript
// Node.js 22の新機能活用例
import { glob } from 'node:fs';
import { parseArgs } from 'node:util';
import { test } from 'node:test';

// require()でのESMサポート
const esmModule = require('./esm-module.mjs');
```

**3. 開発者体験の向上**
- **BrowserView非推奨化**: WebContentViewへの移行推奨
- **@electron/名前空間統一**: パッケージ管理の簡素化
- **Electron Forge 7**: パッケージングツールの刷新

## 個人開発者の実装事例：成功と失敗から学ぶ

### Tauri採用事例の詳細分析

**1. Levminer氏の移行体験[2]**

Levminer氏は、既存のElectronアプリをTauriに移行し、以下の知見を共有しています：

**成功ポイント：**
- **オートアップデーター**: Tauriの実装が格段にシンプル
```rust
// Tauri - 数行で実装完了
tauri::Builder::default()
    .plugin(tauri_plugin_updater::init())
```

- **セキュリティ**: バイナリコンパイルでリバースエンジニアリングが困難
- **配布サイズ**: 85MB → 2.5MB（97%削減）

**苦労した点：**
- 「正直、メモリ使用量の削減は期待ほどではなかった」
- WebView依存による表示差異への対応が必要
- Rust学習に約2週間を要した

**2. Aptabase開発者の選択理由[2]**

フルスタック開発者でデスクトップアプリ経験がなかった開発者の体験：

**Tauriを選んだ決め手：**
- **開発体験**: `npx create-tauri-app`がNext.js並みに洗練されている
- **Rust不要**: 「ほとんどRustを書かずにアプリが完成した」
- **ドキュメント**: 初心者にも分かりやすい構成

```bash
# Tauriアプリの作成（対話形式で設定）
npx create-tauri-app my-app
cd my-app
npm run tauri dev  # 即座に開発開始
```

**3. Hopp社のパフォーマンス要件[2]**

リモートペアプログラミングツール開発での選択：

**要件：**
- 低遅延（50ms以下）のリアルタイム通信
- 最小限のメモリフットプリント
- 高速な画面共有処理

**結果：**
- 6つの同時ウィンドウでのベンチマークでTauriが優位
- ユーザー体験の向上を実現
- ただし、WebRTC実装で苦労（Electronの方が容易）

### Electron継続の合理的判断

**1. 大規模プロダクトでの継続理由**

2024年Stack Overflow調査[1]によると、**60%のクロスプラットフォームアプリ**がElectronを採用。主な理由：

- **Visual Studio Code**: 月間1,400万ユーザー、移行コスト膨大
- **Discord**: リアルタイム通信でElectronのWebRTC実装が優位
- **Slack**: 豊富なサードパーティ統合がElectronで容易

**2. エコシステム依存の実例**

あるSaaS企業の判断（2024年）：
```javascript
// 依存している重要なElectronプラグイン
const criticalDependencies = [
  'electron-builder',      // 高度なビルド設定
  'electron-updater',      // 差分アップデート
  'electron-store',        // 設定管理
  'electron-log',          // ロギング
  'electron-devtools-installer', // 開発ツール
  '@electron/remote',      // レガシーAPI互換
];

// Tauri移行コスト評価
const migrationCost = {
  rewriteTime: '3-6ヶ月',
  testingTime: '2ヶ月',
  riskLevel: 'HIGH',
  roi: 'NEGATIVE' // 既存顧客ベースでは不要
};
```

## セキュリティ：見落としがちな重要ポイント

### Tauriのセキュリティアーキテクチャ

**1. Rust言語による安全性保証[1][3]**

Rustのメモリ安全性がシステムレベルで保証されます：

```rust
// Tauriコマンドは型安全
#[tauri::command]
fn read_file(path: String) -> Result<String, String> {
    // パス検証が自動的に行われる
    if !path.starts_with("/allowed/") {
        return Err("Unauthorized path".to_string());
    }
    // メモリ安全な読み取り
    std::fs::read_to_string(path)
        .map_err(|e| e.to_string())
}
```

**2. サンドボックス化とCSP（Content Security Policy）[5]**

```html
<!-- Tauri - デフォルトで厳格なCSP -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self'">
```

**3. 最小権限原則の実装[1]**

```json
// tauri.conf.json - 明示的な権限設定
{
  "tauri": {
    "allowlist": {
      "all": false,  // デフォルトですべて無効
      "fs": {
        "readFile": true,
        "writeFile": false,
        "scope": ["$APPDATA/*"]
      }
    }
  }
}
```

### Electronのセキュリティ対策

**1. Node.js APIのリスク管理[1]**

Electronでは強力だが危険なAPIへのアクセスに注意が必要：

```javascript
// 悪い例 - セキュリティリスク
webPreferences: {
  nodeIntegration: true,  // 危険！
  contextIsolation: false  // 危険！
}

// 良い例 - セキュアな設定
webPreferences: {
  nodeIntegration: false,
  contextIsolation: true,
  preload: path.join(__dirname, 'preload.js')
}
```

**2. プリロードスクリプトでの安全な通信**

```javascript
// preload.js - 安全なIPC通信
const { contextBridge, ipcRenderer } = require('electron');

contextBridge.exposeInMainWorld('api', {
  readFile: (path) => ipcRenderer.invoke('read-file', path),
  // 検証はメインプロセスで実施
});
```

**3. 定期的なセキュリティアップデート[4]**

Chromiumの脆弱性修正が定期的に提供されるが、アプリ側での更新が必要：

```json
// package.json - 常に最新版を使用
{
  "devDependencies": {
    "electron": "^34.0.0"  // 脆弱性修正を含む最新版
  }
}
```

## 開発体験：学習曲線とプロダクティビティ

### 初期セットアップの比較

**Tauriのセットアップ（所要時間：約15分）**

```bash
# 1. 前提条件のインストール
# Rust（必須）
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 2. Tauriアプリの作成
npx create-tauri-app my-tauri-app
# 対話形式で設定（フレームワーク選択、TypeScript等）

# 3. 開発開始
cd my-tauri-app
npm install
npm run tauri dev  # ホットリロード付き開発サーバー
```

初回ビルドには10-15分かかりますが、その後は高速です。

**Electronのセットアップ（所要時間：約5分）**

```bash
# 1. プロジェクト作成
npx create-electron-app my-electron-app
cd my-electron-app

# 2. 即座に開発開始
npm start  # すぐに起動
```

Node.jsさえあれば即座に開始できる手軽さが魅力です。

### デバッグとテストの効率性

**Tauriのデバッグ体験**

```rust
// Rustバックエンドのデバッグ
#[tauri::command]
fn process_data(input: String) -> Result<String, String> {
    println!("Debug: Processing {}", input);  // コンソール出力
    dbg!(&input);  // 詳細デバッグ情報
    
    // エラーハンドリング
    match complex_operation(input) {
        Ok(result) => Ok(result),
        Err(e) => {
            eprintln!("Error: {}", e);
            Err(e.to_string())
        }
    }
}
```

フロントエンドは通常のWeb開発と同じくChrome DevToolsが使用可能です。

**Electronのデバッグ体験**

```javascript
// メインプロセスのデバッグ
const { app } = require('electron');

app.on('ready', () => {
  // Chrome DevToolsを自動で開く
  mainWindow.webContents.openDevTools();
  
  // VS Codeでのブレークポイントデバッグも可能
  console.log('Debug: App started');
});

// レンダラープロセス（通常のWeb開発と同じ）
console.log('Renderer process debug');
debugger;  // ブレークポイント
```

### CI/CDパイプラインの構築

**Tauri用GitHub Actions設定**

```yaml
name: Build Tauri App
on: [push, pull_request]

jobs:
  build:
    strategy:
      matrix:
        platform: [macos-latest, ubuntu-latest, windows-latest]
    runs-on: ${{ matrix.platform }}
    
    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-node@v3
    - uses: dtolnay/rust-toolchain@stable
    
    - name: Install dependencies (Ubuntu)
      if: matrix.platform == 'ubuntu-latest'
      run: |
        sudo apt-get update
        sudo apt-get install -y libgtk-3-dev webkit2gtk-4.0
    
    - name: Build
      run: |
        npm install
        npm run tauri build
    
    - uses: actions/upload-artifact@v3
      with:
        name: ${{ matrix.platform }}-build
        path: src-tauri/target/release/bundle/
```

**Electron用GitHub Actions設定**

```yaml
name: Build Electron App
on: [push, pull_request]

jobs:
  build:
    strategy:
      matrix:
        os: [macos-latest, ubuntu-latest, windows-latest]
    runs-on: ${{ matrix.os }}
    
    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-node@v3
      with:
        node-version: '20'
    
    - name: Install and Build
      run: |
        npm install
        npm run make
    
    - uses: actions/upload-artifact@v3
      with:
        name: ${{ matrix.os }}-build
        path: out/make/
```

## エコシステムとコミュニティ

### プラグイン・ライブラリの充実度

**Tauri公式プラグイン（2024年時点）[6]**

| カテゴリ | プラグイン数 | 主要プラグイン |
|---------|------------|--------------|
| システム | 15+ | fs, shell, process, clipboard |
| UI/UX | 10+ | dialog, notification, window |
| モバイル | 8+ | biometric, nfc, barcode |
| データ | 5+ | sql, store, stronghold |
| ネットワーク | 5+ | websocket, http, upload |

**Electronエコシステム**

| カテゴリ | パッケージ数 | 主要パッケージ |
|---------|------------|---------------|
| ビルド | 100+ | electron-builder, electron-forge |
| 開発ツール | 200+ | electron-devtools-installer |
| UI | 500+ | electron-window-state, electron-context-menu |
| ユーティリティ | 1000+ | electron-store, electron-log |

### コミュニティサポート

**比較表：**

| 項目 | Electron | Tauri |
|------|----------|--------|
| **GitHub Stars** | 112k+ | 82k+ |
| **月間NPMダウンロード** | 4M+ | 150k+ |
| **Stack Overflow質問数** | 15,000+ | 500+ |
| **日本語記事（Qiita）** | 2,000+ | 100+ |
| **公式Discord** | 10,000+メンバー | 5,000+メンバー |
| **商用サポート** | 複数企業 | CrabNebula社 |

**日本語リソースの充実度**

Electronの方が圧倒的に日本語情報が豊富です[5]：
- Zenn記事: Electron 500+、Tauri 50+
- 技術書: Electron 5冊以上、Tauri 1冊
- 企業採用事例: Electron多数、Tauri少数

## 2025年の選択基準：あなたに最適なフレームワークは？

### Tauriを選ぶべき5つのケース

**1. 軽量・高速アプリが必須要件**
- ユーザーのPCスペックが限定的
- 常駐アプリでメモリ使用量を最小化したい
- 起動時間500ms以下が要求される

**2. セキュリティが最優先事項**
- 金融・医療系アプリケーション
- 機密データを扱うツール
- エンタープライズ向けソリューション

**3. モバイル展開を視野に入れている**
```toml
# Tauri 2.0 - 単一設定でマルチプラットフォーム
[tauri.bundle]
identifier = "com.example.app"
targets = ["deb", "app", "dmg", "msi", "apk", "ipa"]
```

**4. 配布サイズが制約となる環境**
- 帯域幅制限のある地域向け
- 頻繁なアップデートが必要
- ストレージ容量が限られた環境

**5. Rust学習に投資できる**
- 長期的なスキル向上を目指す
- システムプログラミングに興味がある
- パフォーマンス最適化を追求したい

### Electronが適している5つのシナリオ

**1. 迅速なプロトタイピングが必要**
```javascript
// 1日でMVPを作成可能
const { app, BrowserWindow } = require('electron');
app.on('ready', () => {
  new BrowserWindow().loadURL('https://your-webapp.com');
});
```

**2. 豊富なnpmパッケージに依存**
- 特定のElectron専用ライブラリが必須
- 既存のNode.jsコードベースを活用
- サードパーティ統合が多い

**3. チーム全員がJavaScript専門**
- Rust学習の時間的余裕がない
- 既存のスキルセットを最大活用
- 開発速度を最優先

**4. UI一貫性が絶対条件**
- ピクセルパーフェクトなデザイン要求
- 全OS で完全に同一の表示
- 複雑なアニメーション実装

**5. 既存Electronアプリの保守・拡張**
- 移行コストがメリットを上回る
- 安定稼働中のプロダクト
- 顧客基盤が確立済み

## 実装ロードマップ：今すぐ始めるための具体的ステップ

### Tauriスタートガイド

**最初の1週間でやること：**

```markdown
Day 1-2: 環境構築とHello World
- Rustインストール（rustup.rs）
- create-tauri-appでプロジェクト作成
- 基本的なIPC通信の理解

Day 3-4: フロントエンド統合
- お好みのフレームワーク（React/Vue/Svelte）設定
- ホットリロード環境の構築
- 開発ツールの設定

Day 5-6: Rustコマンド実装
- ファイル操作
- システム情報取得
- エラーハンドリング

Day 7: ビルドとパッケージング
- 各OS向けビルド設定
- アイコン・メタデータ設定
- 配布パッケージ作成
```

**避けるべき落とし穴：**

1. **WebView差異を軽視しない**
```css
/* Safari（macOS）では動作しない可能性 */
.container {
  scrollbar-width: thin; /* Firefox only */
  aspect-ratio: 16/9;    /* Safari 15+必要 */
}
```

2. **過度なRust最適化を避ける**
```rust
// 初期は動作優先、最適化は後回し
#[tauri::command]
fn simple_command() -> String {
    "Keep it simple at first".to_string()
}
```

### Electron移行・継続ガイド

**段階的移行戦略（既存Electronアプリの場合）：**

```markdown
Phase 1: 評価（1-2週間）
- パフォーマンスボトルネック特定
- 依存ライブラリのTauri対応確認
- ROI計算

Phase 2: プロトタイプ（2-4週間）
- コア機能のTauri実装
- パフォーマンス比較測定
- ユーザーテスト

Phase 3: 移行判断
- 継続 or 移行の最終決定
- 移行の場合は6ヶ月計画策定
```

**最適化のポイント（Electron継続の場合）：**

```javascript
// 1. メモリリーク対策
window.addEventListener('beforeunload', () => {
  // リスナーやタイマーのクリーンアップ
  clearAllIntervals();
  removeAllListeners();
});

// 2. レンダラープロセス最適化
const { app } = require('electron');
app.commandLine.appendSwitch('disable-gpu');  // GPU無効化
app.commandLine.appendSwitch('disable-software-rasterizer');

// 3. プリロード最適化
// 必要な機能のみ露出
contextBridge.exposeInMainWorld('api', {
  // 最小限のAPI
});
```

## まとめ：2025年以降の展望と推奨事項

2025年のデスクトップアプリ開発において、**ElectronとTauriは共存する**ことが明確になりました。Tauriの採用率は前年比**35%成長**[6]を遂げていますが、Electronも**60%の市場シェア**[1]を維持し、両者にはそれぞれ明確な強みがあります。

**技術トレンドから見る将来性：**
- **Rust採用の加速**: システムレベルの安全性需要は増加傾向
- **モバイル統合**: Tauri 2.0のクロスプラットフォーム対応が新たな可能性を開く
- **AI統合**: 両フレームワークともローカルLLM実行への対応を進める

**最終的な選択指針：**

**Tauriを選ぶべき場合**：パフォーマンス要件が厳しく、将来的な拡張性を重視し、学習投資が可能な個人開発者

**Electronを選ぶべき場合**：開発速度を最優先し、豊富なエコシステムを活用したい、既存のJavaScriptスキルを最大限活かしたい開発者

**次のアクションステップ：**
1. 本記事の選択フローチャートで自己診断
2. 該当フレームワークの公式チュートリアル実施（各1日）
3. 小規模プロトタイプ作成で実感を得る
4. コミュニティ参加で最新情報をキャッチアップ

技術選択に「絶対的な正解」はありません。あなたのプロジェクト要件、スキルセット、そして将来のビジョンに基づいて、最適な選択をしてください。

## 参考文献

[1] Tauri vs Electron: A 2025 Comparison for Desktop Development - Codeology (2025)

[2] 個人開発者の実装事例集 - Levminer, Aptabase開発者レポート (2024)

[3] Tauri 2.0 公式リリースノート - Tauri.app (2024)

[4] Electron 34.0.0 リリース情報 - Electronjs.org (2024)

[5] 日本語技術記事 - Zenn, Publickey (2024)

[6] Tauri Ecosystem - GitHub awesome-tauri (2024)

[7] Electron Ecosystem Node.js 22移行計画 - Electronjs.org (2025)

---

*本記事は2025年8月24日時点の情報に基づいています。技術は日々進化しているため、最新の公式ドキュメントも併せてご確認ください。*