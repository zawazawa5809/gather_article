---
permalink: /single-html-cdn-guide
title: "【2025年最新】単一HTMLで作成するドキュメントに使える人気のあるCDN20選とデモコード完全ガイド"
summary: "ビルド不要！単一HTMLファイルでモダンWeb開発を始めるための、信頼性の高いCDNライブラリ20選を2025年最新情報でお届け。Bootstrap、GSAP、Three.jsなど実用的なデモコード付きで今すぐ使える。"
tags:
  - "#web-development"
  - "#cdn"
  - "#html"
  - "#frontend"
  - "#javascript"
  - "#productivity"
---

# 【2025年最新】単一HTMLで作成するドキュメントに使える人気のあるCDN20選とデモコード完全ガイド

## はじめに

モダンなWeb開発において、複雑なビルドプロセスやパッケージ管理に悩まされることなく、すぐに美しく機能的なWebページを作成したいと考えたことはありませんか？単一HTMLドキュメント開発は、そんな開発者のニーズに応える最適なソリューションです。

単一HTMLファイルでの開発とは、HTML、CSS、JavaScriptを1つのファイルに統合し、外部依存関係をCDN（Content Delivery Network）[^1]経由で読み込む開発手法です。この手法により、npm installも、webpackの設定も、複雑なディレクトリ構成も不要になります。

2025年現在、Web開発の複雑化が進む一方で、プロトタイピング、教育用途、シンプルなランディングページ制作において、この手法の価値が再評価されています。特に、CDN技術の進歩により、信頼性とパフォーマンスが大幅に向上し、本格的な開発にも十分活用できるレベルに達しています。

本記事では、2025年最新の情報に基づき、単一HTMLドキュメント開発で活用できる信頼性の高いCDNライブラリを厳選して20個ご紹介します。各ライブラリには、コピー&ペーストで即座に動作するHTMLデモコードを付属させ、すぐに実践に移せる内容となっています。

[^1]: CDN（Content Delivery Network）: 世界中に分散配置されたサーバーネットワークを通じて、Webコンテンツを高速かつ安定的に配信するシステム

## CDNの基礎知識

### CDNとは何か

CDN（Content Delivery Network）は、静的リソース（JavaScriptライブラリ、CSSフレームワーク、画像など）を地理的に分散したサーバーネットワークから配信するシステムです。従来の単一サーバーでの配信と比較して、ユーザーに最も近いサーバーからコンテンツを提供することで、読み込み速度の向上とサーバー負荷の分散を実現します。

Web開発においてCDNを使用する主なメリットは以下の通りです：

**パフォーマンス向上**: 地理的に近いサーバーからの配信により、レイテンシが大幅に削減されます。
**信頼性の向上**: 複数のサーバーでの冗長化により、単一障害点を排除します。
**開発効率の向上**: ライブラリの管理やバージョン更新が自動化されます。
**帯域幅コストの削減**: 自社サーバーの負荷を軽減し、運用コストを抑制できます。

### 2025年の主要CDNプロバイダ比較

2025年現在、Web開発で広く利用されているCDNプロバイダを比較してみましょう。

| CDNプロバイダ | 運営組織 | 月間リクエスト数 | 主な特徴 | 信頼性スコア |
|---|---|---|---|---|
| **jsDelivr** | ProspectOne | 1,500億+ | npm/GitHub統合、ESMサポート | 10/10 |
| **cdnjs** | Cloudflare | 2,000億+ | 豊富なライブラリ、高速配信 | 10/10 |
| **unpkg** | Michael Jackson | 非公開 | npm直接配信、シンプル | 8/10 |
| **Google Fonts** | Google | 非公開 | フォント特化、高品質 | 9/10 |

*表1: 主要CDNプロバイダの比較（2025年最新データ）*

**jsDelivr**[^2]は、npm とGitHubから直接パッケージを配信する無料CDNサービスで、ESモジュール（ES Modules）[^3]にも対応しており、モダンなJavaScript開発に最適化されています。

**cdnjs**[^4]は、Cloudflareが運営する最大級のオープンソースCDNサービスで、Webサイトの12.5%以上が利用している業界標準のサービスです。

**unpkg**[^5]は、npmレジストリから直接パッケージを配信するシンプルなCDNで、特定のバージョンやファイルへの直接アクセスが容易です。

[^2]: jsDelivr: https://www.jsdelivr.com/ - 無料CDN、月間1,500億リクエスト処理、npm/GitHub統合
[^3]: ESモジュール: ECMAScript 2015で標準化されたJavaScriptのモジュールシステム
[^4]: cdnjs: https://cdnjs.com - Cloudflare製CDN、12.5%サイト利用、月間2,000億リクエスト
[^5]: unpkg: https://unpkg.com - npm パッケージ直接配信CDN

### 単一HTMLでCDNを使う際の注意点

単一HTMLドキュメントでCDNを効果的に活用するためには、以下の点に注意が必要です：

**バージョン固定の重要性**: `@latest`を使用すると予期しない破壊的変更が発生する可能性があります。本番環境では特定のバージョンを指定することを強く推奨します。

**読み込み順序の管理**: 依存関係のあるライブラリは正しい順序で読み込む必要があります。例えば、Bootstrap 4ではjQuery → Popper.js → Bootstrapの順序が必要です。

**フォールバック戦略**: CDNが利用できない場合に備えて、複数のCDNを設定するか、ローカルファイルへのフォールバックを検討してください。

**セキュリティ対策**: Subresource Integrity（SRI）[^6]を使用して、配信されるファイルの整合性を検証することを推奨します。

**パフォーマンス最適化**: 必要なファイルのみを読み込み、minified版を選択してください。また、preload やprefetch ディレクティブの活用も効果的です。

[^6]: SRI（Subresource Integrity）: ブラウザがファイルの改ざんを検出するためのセキュリティ機能

## CSSフレームワーク系CDN（5選）

### Bootstrap 5.3.7 - 世界標準のレスポンシブフレームワーク

Bootstrap[^7]は、2011年にTwitter社（現X社）で開発された世界最も人気のあるCSSフレームワークです。2025年現在、Bootstrap 5系がメインストリームとなり、jQuery依存を完全に排除し、よりモダンな開発体験を提供しています。

**特徴**:
- jQuery不要の軽量設計
- CSS Gridとflexboxベースのレスポンシブシステム
- 豊富なコンポーネントライブラリ
- カスタマイズ性の高いCSS変数設計
- アクセシビリティ（WCAG 2.1 AA準拠）への強いコミット

**信頼性スコア**: 10/10（公式サポート・高頻度更新・広範囲利用実績）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap 5 デモ</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor" crossorigin="anonymous">
</head>
<body>
    <div class="container mt-5">
        <div class="row">
            <div class="col-lg-8 mx-auto">
                <h1 class="text-primary mb-4">Bootstrap 5 デモページ</h1>
                <div class="card">
                    <div class="card-header">
                        <h5 class="card-title mb-0">レスポンシブカード</h5>
                    </div>
                    <div class="card-body">
                        <p class="card-text">Bootstrap 5では、jQuery依存を完全に排除し、ピュアJavaScriptで動作します。</p>
                        <button class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal">
                            モーダルを開く
                        </button>
                        <button class="btn btn-outline-info ms-2" data-bs-toggle="collapse" data-bs-target="#collapseExample">
                            コラプス切り替え
                        </button>
                    </div>
                </div>
                
                <div class="collapse mt-3" id="collapseExample">
                    <div class="alert alert-info">
                        これはBootstrap 5のコラプス機能です。jQueryなしで動作します！
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Bootstrap 5 モーダル</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <p>Bootstrap 5の新機能をお試しください。</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">閉じる</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>
</body>
</html>
```

[^7]: Bootstrap: https://getbootstrap.com/ - 世界最人気CSSフレームワーク、レスポンシブデザイン

### Tailwind CSS Play CDN - ユーティリティファーストの新時代

Tailwind CSS[^8]は、ユーティリティファースト（Utility-First）[^9]のアプローチを採用した革新的なCSSフレームワークです。従来のコンポーネントベースのフレームワークとは異なり、小さなユーティリティクラスを組み合わせてデザインを構築します。

**特徴**:
- 原子的なユーティリティクラス設計
- 高度なカスタマイズ性
- パフォーマンス最適化（未使用クラスの自動削除）
- ダークモード対応
- 開発環境での即座のプロトタイピング支援

**信頼性スコア**: 9/10（公式・開発用途限定のPlay CDN）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailwind CSS デモ</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'brand-blue': '#1e40af',
                        'brand-green': '#10b981'
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-gray-100 min-h-screen">
    <div class="container mx-auto px-4 py-8">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-4xl font-bold text-brand-blue mb-8 text-center">
                Tailwind CSS デモページ
            </h1>
            
            <div class="grid md:grid-cols-2 gap-6">
                <!-- カード1 -->
                <div class="bg-white rounded-lg shadow-lg overflow-hidden transform hover:scale-105 transition-transform duration-300">
                    <div class="bg-gradient-to-r from-blue-500 to-purple-600 h-48 flex items-center justify-center">
                        <h2 class="text-white text-2xl font-semibold">グラデーション</h2>
                    </div>
                    <div class="p-6">
                        <p class="text-gray-600 mb-4">Tailwindの美しいグラデーション機能をお試しください。</p>
                        <button class="bg-brand-green hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full transition-colors duration-200">
                            詳細を見る
                        </button>
                    </div>
                </div>

                <!-- カード2 -->
                <div class="bg-white rounded-lg shadow-lg overflow-hidden">
                    <div class="p-6">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 bg-yellow-400 rounded-full flex items-center justify-center">
                                <span class="text-xl">🚀</span>
                            </div>
                            <h3 class="ml-4 text-xl font-semibold text-gray-800">高速開発</h3>
                        </div>
                        <p class="text-gray-600 mb-4">ユーティリティクラスで素早くプロトタイプを作成できます。</p>
                        <div class="space-y-2">
                            <div class="w-full bg-gray-200 rounded-full h-2">
                                <div class="bg-blue-600 h-2 rounded-full w-3/4"></div>
                            </div>
                            <div class="flex justify-between text-sm text-gray-500">
                                <span>開発効率</span>
                                <span>75%</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- レスポンシブグリッド -->
            <div class="mt-8 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="bg-red-100 p-4 rounded text-center">
                    <div class="text-red-600 text-2xl mb-2">📱</div>
                    <div class="text-sm text-red-800">モバイル</div>
                </div>
                <div class="bg-blue-100 p-4 rounded text-center">
                    <div class="text-blue-600 text-2xl mb-2">💻</div>
                    <div class="text-sm text-blue-800">タブレット</div>
                </div>
                <div class="bg-green-100 p-4 rounded text-center">
                    <div class="text-green-600 text-2xl mb-2">🖥️</div>
                    <div class="text-sm text-green-800">デスクトップ</div>
                </div>
                <div class="bg-purple-100 p-4 rounded text-center">
                    <div class="text-purple-600 text-2xl mb-2">📺</div>
                    <div class="text-sm text-purple-800">大画面</div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
```

**注意**: Play CDNは開発・プロトタイピング用途に限定されています。本番環境では適切なビルドプロセスを使用してください。

[^8]: Tailwind CSS: https://tailwindcss.com/ - ユーティリティファーストCSSフレームワーク
[^9]: ユーティリティファースト: 小さな単機能クラスを組み合わせてスタイルを構築する設計思想

### Font Awesome 6系 - アイコンライブラリの決定版

Font Awesome[^10]は、Web開発において最も広く使用されているアイコンライブラリです。2025年現在、6,000個を超えるアイコンを提供し、SVG、Webフォント、CSS の複数の形式に対応しています。

**特徴**:
- 豊富なアイコンセット（6,000+）
- SVGとWebフォントの両方に対応
- 高解像度ディスプレイ対応
- アクセシビリティ機能内蔵
- アニメーション効果対応

**信頼性スコア**: 10/10（公式・豊富なアイコン）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Font Awesome デモ</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous">
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: white;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        .icon-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        .icon-card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .icon-large {
            font-size: 3rem;
            margin-bottom: 10px;
            display: block;
        }
        .social-links {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 30px 0;
        }
        .social-links a {
            color: white;
            font-size: 2rem;
            transition: transform 0.3s ease;
        }
        .social-links a:hover {
            transform: scale(1.2);
        }
        .animation-demo {
            text-align: center;
            margin: 40px 0;
        }
        .spin { animation: fa-spin 2s infinite linear; }
        .pulse { animation: fa-beat 1s infinite; }
    </style>
</head>
<body>
    <div class="container">
        <h1 style="text-align: center; margin-bottom: 10px;">
            <i class="fas fa-star"></i> Font Awesome 6 デモ <i class="fas fa-star"></i>
        </h1>
        <p style="text-align: center; opacity: 0.9;">6,000+のアイコンライブラリを体験</p>

        <!-- ソーシャルメディアアイコン -->
        <div class="social-links">
            <a href="#" title="Facebook"><i class="fab fa-facebook"></i></a>
            <a href="#" title="Twitter"><i class="fab fa-twitter"></i></a>
            <a href="#" title="Instagram"><i class="fab fa-instagram"></i></a>
            <a href="#" title="LinkedIn"><i class="fab fa-linkedin"></i></a>
            <a href="#" title="GitHub"><i class="fab fa-github"></i></a>
            <a href="#" title="YouTube"><i class="fab fa-youtube"></i></a>
        </div>

        <!-- アイコンカテゴリ -->
        <div class="icon-grid">
            <div class="icon-card">
                <i class="fas fa-home icon-large"></i>
                <h3>ナビゲーション</h3>
                <p><i class="fas fa-home"></i> ホーム　<i class="fas fa-user"></i> プロフィール　<i class="fas fa-cog"></i> 設定</p>
            </div>

            <div class="icon-card">
                <i class="fas fa-envelope icon-large"></i>
                <h3>コミュニケーション</h3>
                <p><i class="fas fa-envelope"></i> メール　<i class="fas fa-phone"></i> 電話　<i class="fas fa-comment"></i> チャット</p>
            </div>

            <div class="icon-card">
                <i class="fas fa-shopping-cart icon-large"></i>
                <h3>Eコマース</h3>
                <p><i class="fas fa-shopping-cart"></i> カート　<i class="fas fa-credit-card"></i> 決済　<i class="fas fa-truck"></i> 配送</p>
            </div>

            <div class="icon-card">
                <i class="fas fa-chart-bar icon-large"></i>
                <h3>データ・分析</h3>
                <p><i class="fas fa-chart-bar"></i> グラフ　<i class="fas fa-database"></i> データ　<i class="fas fa-analytics"></i> 分析</p>
            </div>
        </div>

        <!-- アニメーション機能 -->
        <div class="animation-demo">
            <h2>アニメーション機能</h2>
            <div style="font-size: 2rem; margin: 20px 0;">
                <i class="fas fa-spinner spin" style="margin: 0 10px;"></i>
                <i class="fas fa-heart pulse" style="margin: 0 10px; color: #ff6b6b;"></i>
                <i class="fas fa-star fa-beat" style="margin: 0 10px; color: #ffd93d;"></i>
                <i class="fas fa-bell fa-shake" style="margin: 0 10px; color: #6bcf7f;"></i>
            </div>
            <p style="opacity: 0.9;">CSS アニメーションクラスでアイコンに動きを追加</p>
        </div>

        <!-- 実用例 -->
        <div style="background: rgba(255, 255, 255, 0.1); padding: 20px; border-radius: 10px; margin-top: 30px;">
            <h3><i class="fas fa-lightbulb"></i> 実用的な使用例</h3>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-top: 15px;">
                <div><i class="fas fa-check-circle" style="color: #4ecdc4;"></i> 成功メッセージ</div>
                <div><i class="fas fa-exclamation-triangle" style="color: #ffe66d;"></i> 警告表示</div>
                <div><i class="fas fa-times-circle" style="color: #ff6b6b;"></i> エラー通知</div>
                <div><i class="fas fa-info-circle" style="color: #74b9ff;"></i> 情報表示</div>
            </div>
        </div>
    </div>
</body>
</html>
```

[^10]: Font Awesome: https://fontawesome.com/ - 世界最大級のアイコンライブラリ

### Animate.css 4.1.1 - CSS アニメーションを簡単に

Animate.css[^11]は、ready-to-use（すぐに使える）CSSアニメーションライブラリです。複雑なCSSアニメーションを記述することなく、クラス名を追加するだけで美しいアニメーション効果を実現できます。

**特徴**:
- 80以上のアニメーション効果
- クロスブラウザ対応
- 軽量設計（最小2KB）
- カスタマイズ可能なデュレーション
- JavaScript APIとの親和性

**信頼性スコア**: 9/10（軽量・豊富なアニメーション）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animate.css デモ</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" integrity="sha512-c3SN6fOj/TT2Vv0/5yjE7TpB4bhGu2d1g/bBBAJr5ht8mQMJaOfM0TgPwKgAHa3PgI0JMQTw7JEhSNe6W4YJsQ==" crossorigin="anonymous">
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            min-height: 100vh;
            color: white;
        }
        .container {
            max-width: 1000px;
            margin: 0 auto;
            text-align: center;
        }
        .demo-box {
            display: inline-block;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 10px;
            padding: 20px;
            margin: 10px;
            min-width: 150px;
            cursor: pointer;
            transition: background 0.3s ease;
        }
        .demo-box:hover {
            background: rgba(255, 255, 255, 0.2);
        }
        .animation-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        .control-panel {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 20px;
            margin: 30px 0;
        }
        button {
            background: #4ecdc4;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 5px;
            font-size: 14px;
            transition: background 0.3s ease;
        }
        button:hover {
            background: #45b7aa;
        }
        .hero-section {
            padding: 40px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- ヒーローセクション -->
        <div class="hero-section">
            <h1 class="animate__animated animate__bounceInDown">
                Animate.css デモページ
            </h1>
            <p class="animate__animated animate__fadeInUp animate__delay-1s">
                クラス名を追加するだけで美しいアニメーションを実現
            </p>
        </div>

        <!-- アニメーション体験セクション -->
        <div class="control-panel">
            <h2>アニメーションを体験してみよう</h2>
            <div id="animationTarget" class="demo-box">
                <h3>🎭</h3>
                <p>ここがアニメーションします</p>
            </div>
            <div style="margin-top: 20px;">
                <button onclick="playAnimation('bounceIn')">Bounce In</button>
                <button onclick="playAnimation('fadeInLeft')">Fade In Left</button>
                <button onclick="playAnimation('rotateIn')">Rotate In</button>
                <button onclick="playAnimation('zoomIn')">Zoom In</button>
                <button onclick="playAnimation('slideInUp')">Slide In Up</button>
                <button onclick="playAnimation('heartBeat')">Heart Beat</button>
                <button onclick="playAnimation('wobble')">Wobble</button>
                <button onclick="playAnimation('jello')">Jello</button>
            </div>
        </div>

        <!-- カテゴリ別アニメーション -->
        <div class="animation-grid">
            <div class="demo-box animate__animated animate__pulse animate__infinite">
                <h3>🔄 注意喚起</h3>
                <p>pulse (無限ループ)</p>
            </div>

            <div class="demo-box animate__animated animate__bounce">
                <h3>🎾 エントランス</h3>
                <p>bounce</p>
            </div>

            <div class="demo-box animate__animated animate__rubberBand">
                <h3>🎪 強調効果</h3>
                <p>rubberBand</p>
            </div>

            <div class="demo-box animate__animated animate__shakeX">
                <h3>⚡ エラー表示</h3>
                <p>shakeX</p>
            </div>
        </div>

        <!-- スクロール連動デモ -->
        <div style="height: 100vh; display: flex; align-items: center; justify-content: center;">
            <div id="scrollTarget" style="opacity: 0;">
                <h2>スクロールでアニメーション発動！</h2>
                <p>Intersection Observer API との組み合わせ例</p>
            </div>
        </div>

        <!-- 実用例 -->
        <div style="background: rgba(255, 255, 255, 0.1); padding: 30px; border-radius: 10px; margin: 30px 0;">
            <h2>実用的な使用例</h2>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-top: 20px;">
                <div class="demo-box" onclick="showNotification()">
                    <h4>通知表示</h4>
                    <p>クリックして通知を表示</p>
                </div>
                <div class="demo-box" onclick="toggleModal()">
                    <h4>モーダル表示</h4>
                    <p>スムーズなモーダル表示</p>
                </div>
                <div class="demo-box" onclick="animateProgress()">
                    <h4>プログレス表示</h4>
                    <p>読み込み状況の表示</p>
                </div>
            </div>
        </div>
    </div>

    <!-- 通知エリア -->
    <div id="notification" style="position: fixed; top: 20px; right: 20px; background: #4ecdc4; color: white; padding: 15px; border-radius: 5px; display: none;">
        通知メッセージが表示されました！
    </div>

    <!-- プログレスバー -->
    <div id="progressBar" style="position: fixed; bottom: 0; left: 0; height: 4px; background: #4ecdc4; width: 0%; transition: width 2s ease; display: none;"></div>

    <script>
        // アニメーションを再生する関数
        function playAnimation(animationName) {
            const target = document.getElementById('animationTarget');
            target.className = 'demo-box';
            
            // 少し遅延させてからアニメーションを適用
            setTimeout(() => {
                target.classList.add('animate__animated', `animate__${animationName}`);
            }, 100);

            // アニメーション終了後にクラスを削除
            target.addEventListener('animationend', function() {
                target.classList.remove('animate__animated', `animate__${animationName}`);
            }, { once: true });
        }

        // 通知表示
        function showNotification() {
            const notification = document.getElementById('notification');
            notification.style.display = 'block';
            notification.classList.add('animate__animated', 'animate__slideInRight');
            
            setTimeout(() => {
                notification.classList.remove('animate__slideInRight');
                notification.classList.add('animate__slideOutRight');
                setTimeout(() => {
                    notification.style.display = 'none';
                    notification.classList.remove('animate__animated', 'animate__slideOutRight');
                }, 500);
            }, 3000);
        }

        // プログレスアニメーション
        function animateProgress() {
            const progressBar = document.getElementById('progressBar');
            progressBar.style.display = 'block';
            progressBar.style.width = '0%';
            
            setTimeout(() => {
                progressBar.style.width = '100%';
            }, 100);

            setTimeout(() => {
                progressBar.style.display = 'none';
            }, 2500);
        }

        // スクロール連動アニメーション
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.classList.add('animate__animated', 'animate__fadeInUp');
                }
            });
        });

        observer.observe(document.getElementById('scrollTarget'));

        // ページロード時のアニメーション
        window.addEventListener('load', () => {
            // 遅延してアニメーションを開始
            setTimeout(() => {
                document.querySelectorAll('.animation-grid .demo-box').forEach((box, index) => {
                    setTimeout(() => {
                        box.style.opacity = '1';
                        box.classList.add('animate__animated', 'animate__zoomIn');
                    }, index * 200);
                });
            }, 500);
        });
    </script>
</body>
</html>
```

[^11]: Animate.css: https://animate.style/ - ready-to-use CSSアニメーションライブラリ

### Bulma - モダンなFlexboxベースフレームワーク

Bulma[^12]は、Flexboxをベースとした現代的なCSSフレームワークです。JavaScriptコンポーネントを含まないピュアCSSフレームワークとして設計されており、軽量で柔軟性の高い開発体験を提供します。

**特徴**:
- 100% レスポンシブデザイン
- モジュラー設計（必要な部分のみ使用可能）
- Flexboxベースのモダンなレイアウト
- JavaScript依存なし
- シンプルで直感的なクラス名

**信頼性スコア**: 8/10（Flexboxベース・軽量）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bulma デモ</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@1.0.0/css/bulma.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
</head>
<body>
    <!-- ナビゲーション -->
    <nav class="navbar is-primary" role="navigation">
        <div class="navbar-brand">
            <a class="navbar-item">
                <strong>Bulma デモ</strong>
            </a>
            <a role="button" class="navbar-burger" data-target="navbarMenu">
                <span></span>
                <span></span>
                <span></span>
            </a>
        </div>
        <div id="navbarMenu" class="navbar-menu">
            <div class="navbar-start">
                <a class="navbar-item">ホーム</a>
                <a class="navbar-item">機能</a>
                <a class="navbar-item">ドキュメント</a>
            </div>
            <div class="navbar-end">
                <div class="navbar-item">
                    <div class="buttons">
                        <a class="button is-primary">
                            <strong>サインアップ</strong>
                        </a>
                        <a class="button is-light">ログイン</a>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- ヒーローセクション -->
    <section class="hero is-info is-medium">
        <div class="hero-body">
            <div class="container">
                <h1 class="title">
                    Bulma フレームワーク
                </h1>
                <h2 class="subtitle">
                    モダンなFlexboxベースのCSSフレームワーク
                </h2>
                <a class="button is-white is-large">
                    <span class="icon">
                        <i class="fas fa-download"></i>
                    </span>
                    <span>ダウンロード</span>
                </a>
            </div>
        </div>
    </section>

    <!-- メインコンテンツ -->
    <section class="section">
        <div class="container">
            <div class="columns">
                <!-- サイドバー -->
                <div class="column is-3">
                    <aside class="menu">
                        <p class="menu-label">一般</p>
                        <ul class="menu-list">
                            <li><a class="is-active">ダッシュボード</a></li>
                            <li><a>顧客</a></li>
                        </ul>
                        <p class="menu-label">管理</p>
                        <ul class="menu-list">
                            <li><a>チーム設定</a></li>
                            <li>
                                <a>プロジェクト管理</a>
                                <ul>
                                    <li><a>メンバー</a></li>
                                    <li><a>プラグイン</a></li>
                                    <li><a>新規追加</a></li>
                                </ul>
                            </li>
                        </ul>
                    </aside>
                </div>

                <!-- メインコンテンツ -->
                <div class="column">
                    <h1 class="title">ダッシュボード</h1>
                    
                    <!-- 統計カード -->
                    <div class="columns">
                        <div class="column">
                            <div class="box">
                                <div class="level">
                                    <div class="level-item has-text-centered">
                                        <div>
                                            <p class="heading">ユーザー</p>
                                            <p class="title">3,456</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="column">
                            <div class="box">
                                <div class="level">
                                    <div class="level-item has-text-centered">
                                        <div>
                                            <p class="heading">売上</p>
                                            <p class="title">¥1,234,567</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="column">
                            <div class="box">
                                <div class="level">
                                    <div class="level-item has-text-centered">
                                        <div>
                                            <p class="heading">注文</p>
                                            <p class="title">789</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- フォーム例 -->
                    <div class="box">
                        <h2 class="subtitle">フォーム例</h2>
                        <form>
                            <div class="field">
                                <label class="label">名前</label>
                                <div class="control has-icons-left">
                                    <input class="input" type="text" placeholder="お名前を入力">
                                    <span class="icon is-small is-left">
                                        <i class="fas fa-user"></i>
                                    </span>
                                </div>
                            </div>

                            <div class="field">
                                <label class="label">メール</label>
                                <div class="control has-icons-left has-icons-right">
                                    <input class="input is-success" type="email" placeholder="メールアドレス" value="alex@example.com">
                                    <span class="icon is-small is-left">
                                        <i class="fas fa-envelope"></i>
                                    </span>
                                    <span class="icon is-small is-right">
                                        <i class="fas fa-check"></i>
                                    </span>
                                </div>
                                <p class="help is-success">このメールアドレスは有効です</p>
                            </div>

                            <div class="field">
                                <label class="label">メッセージ</label>
                                <div class="control">
                                    <textarea class="textarea" placeholder="メッセージを入力"></textarea>
                                </div>
                            </div>

                            <div class="field is-grouped">
                                <div class="control">
                                    <button class="button is-link">送信</button>
                                </div>
                                <div class="control">
                                    <button class="button is-link is-light">キャンセル</button>
                                </div>
                            </div>
                        </form>
                    </div>

                    <!-- 通知例 -->
                    <div class="notification is-success">
                        <button class="delete"></button>
                        <strong>成功！</strong> データが正常に保存されました。
                    </div>

                    <div class="notification is-warning">
                        <button class="delete"></button>
                        <strong>注意：</strong> この操作は元に戻せません。
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- フッター -->
    <footer class="footer">
        <div class="content has-text-centered">
            <p>
                <strong>Bulma</strong> by <a href="https://jgthms.com">Jeremy Thomas</a>. 
                The source code is licensed <a href="http://opensource.org/licenses/mit-license.php">MIT</a>.
            </p>
        </div>
    </footer>

    <script>
        // ナビゲーションバーガーメニューの制御
        document.addEventListener('DOMContentLoaded', () => {
            const $navbarBurgers = Array.prototype.slice.call(document.querySelectorAll('.navbar-burger'), 0);
            
            if ($navbarBurgers.length > 0) {
                $navbarBurgers.forEach(el => {
                    el.addEventListener('click', () => {
                        const target = el.dataset.target;
                        const $target = document.getElementById(target);
                        el.classList.toggle('is-active');
                        $target.classList.toggle('is-active');
                    });
                });
            }

            // 通知の削除機能
            const deleteButtons = document.querySelectorAll('.notification .delete');
            deleteButtons.forEach(button => {
                button.addEventListener('click', () => {
                    button.parentElement.style.display = 'none';
                });
            });
        });
    </script>
</body>
</html>
```

[^12]: Bulma: https://bulma.io/ - モダンなFlexboxベースCSSフレームワーク

## JavaScript ライブラリ系CDN（8選）

### jQuery 3系 - 不変のDOM操作ライブラリ

jQuery[^13]は、2006年にJohn Resigによって開発されたJavaScriptライブラリで、Web開発の歴史において最も影響力のあるライブラリの一つです。2025年現在でも、DOM操作、イベント処理、Ajax通信の分野で広く利用されています。

**特徴**:
- クロスブラウザ互換性
- 簡潔で直感的なAPI設計
- 豊富なプラグインエコシステム
- チェーンメソッド対応
- 軽量かつ高速

**信頼性スコア**: 9/10（歴史的信頼性・広範囲対応）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery デモ</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: white;
        }
        .container {
            max-width: 1000px;
            margin: 0 auto;
        }
        .demo-section {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            backdrop-filter: blur(10px);
        }
        .button {
            background: #4ecdc4;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 5px;
            transition: all 0.3s ease;
        }
        .button:hover {
            background: #45b7aa;
            transform: translateY(-2px);
        }
        .animated-box {
            width: 100px;
            height: 100px;
            background: #ff6b6b;
            margin: 20px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .task-item {
            background: rgba(255, 255, 255, 0.2);
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .task-item.completed {
            opacity: 0.6;
            text-decoration: line-through;
        }
        .form-group {
            margin: 15px 0;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        .form-group input, .form-group textarea {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 5px;
            background: rgba(255, 255, 255, 0.9);
            color: #333;
        }
        .gallery img {
            width: 150px;
            height: 100px;
            object-fit: cover;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .gallery img:hover {
            transform: scale(1.1);
        }
        .ajax-content {
            min-height: 100px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 5px;
            padding: 15px;
            margin: 10px 0;
        }
        .loading {
            text-align: center;
            padding: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>jQuery 3.7.1 デモページ</h1>
        <p>Web開発の定番ライブラリjQueryの主要機能をデモンストレーション</p>

        <!-- DOM操作デモ -->
        <div class="demo-section">
            <h2>DOM操作とイベント処理</h2>
            <div style="display: flex; gap: 20px; align-items: center; flex-wrap: wrap;">
                <div class="animated-box" id="animatedBox"></div>
                <div>
                    <button class="button" id="changeColor">色を変更</button>
                    <button class="button" id="animate">アニメーション</button>
                    <button class="button" id="fadeToggle">フェード切り替え</button>
                    <button class="button" id="slideToggle">スライド切り替え</button>
                </div>
            </div>
            <div id="eventLog" style="margin-top: 15px; padding: 10px; background: rgba(0,0,0,0.2); border-radius: 5px; max-height: 100px; overflow-y: auto;"></div>
        </div>

        <!-- フォーム処理デモ -->
        <div class="demo-section">
            <h2>フォーム処理とバリデーション</h2>
            <form id="demoForm">
                <div class="form-group">
                    <label for="username">ユーザー名（必須）:</label>
                    <input type="text" id="username" name="username" required>
                </div>
                <div class="form-group">
                    <label for="email">メールアドレス:</label>
                    <input type="email" id="email" name="email">
                </div>
                <div class="form-group">
                    <label for="message">メッセージ:</label>
                    <textarea id="message" name="message" rows="3"></textarea>
                </div>
                <button type="submit" class="button">送信</button>
                <button type="button" class="button" id="clearForm">クリア</button>
            </form>
            <div id="formResult" style="margin-top: 15px;"></div>
        </div>

        <!-- ToDo リスト -->
        <div class="demo-section">
            <h2>動的コンテンツ操作（ToDo リスト）</h2>
            <div style="display: flex; gap: 10px; margin-bottom: 15px;">
                <input type="text" id="newTask" placeholder="新しいタスクを入力" style="flex: 1; padding: 10px; border: none; border-radius: 5px;">
                <button class="button" id="addTask">追加</button>
            </div>
            <div id="taskList">
                <div class="task-item">
                    <span>jQueryの学習</span>
                    <div>
                        <button class="button" onclick="$(this).parent().parent().toggleClass('completed')">完了</button>
                        <button class="button" onclick="$(this).parent().parent().remove()">削除</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- イメージギャラリー -->
        <div class="demo-section">
            <h2>イベント委任とエフェクト</h2>
            <div class="gallery">
                <img src="https://picsum.photos/150/100?random=1" alt="Sample 1">
                <img src="https://picsum.photos/150/100?random=2" alt="Sample 2">
                <img src="https://picsum.photos/150/100?random=3" alt="Sample 3">
                <img src="https://picsum.photos/150/100?random=4" alt="Sample 4">
            </div>
            <div id="imageInfo" style="margin-top: 15px; font-style: italic;"></div>
        </div>

        <!-- Ajax通信デモ -->
        <div class="demo-section">
            <h2>Ajax通信</h2>
            <button class="button" id="loadData">データを読み込み</button>
            <button class="button" id="loadJSON">JSON データ読み込み</button>
            <div id="ajaxResult" class="ajax-content">
                ここにAjax通信の結果が表示されます
            </div>
        </div>

        <!-- チェーンメソッドデモ -->
        <div class="demo-section">
            <h2>jQueryチェーンメソッド</h2>
            <div id="chainDemo" style="background: #ff6b6b; width: 100px; height: 100px; margin: 20px auto; border-radius: 50%;"></div>
            <button class="button" id="chainAnimation">チェーンアニメーション実行</button>
            <pre style="background: rgba(0,0,0,0.3); padding: 15px; border-radius: 5px; margin-top: 15px; overflow-x: auto;"><code>$('#chainDemo')
  .fadeOut(500)
  .delay(200)
  .fadeIn(500)
  .animate({width: '150px', height: '150px'}, 1000)
  .animate({width: '100px', height: '100px'}, 1000);</code></pre>
        </div>
    </div>

    <script>
        $(document).ready(function() {
            // ログ機能
            function logEvent(message) {
                const timestamp = new Date().toLocaleTimeString();
                $('#eventLog').prepend(`<div>[${timestamp}] ${message}</div>`);
            }

            // DOM操作とイベント処理
            $('#changeColor').click(function() {
                const colors = ['#ff6b6b', '#4ecdc4', '#45b7aa', '#96ceb4', '#feca57', '#ff9ff3'];
                const randomColor = colors[Math.floor(Math.random() * colors.length)];
                $('#animatedBox').css('background-color', randomColor);
                logEvent(`色を${randomColor}に変更`);
            });

            $('#animate').click(function() {
                $('#animatedBox').animate({
                    width: '150px',
                    height: '150px',
                    borderRadius: '50%'
                }, 500).animate({
                    width: '100px',
                    height: '100px',
                    borderRadius: '10px'
                }, 500);
                logEvent('アニメーション実行');
            });

            $('#fadeToggle').click(function() {
                $('#animatedBox').fadeToggle();
                logEvent('フェード切り替え');
            });

            $('#slideToggle').click(function() {
                $('#animatedBox').slideToggle();
                logEvent('スライド切り替え');
            });

            // フォーム処理
            $('#demoForm').submit(function(e) {
                e.preventDefault();
                
                const username = $('#username').val();
                const email = $('#email').val();
                const message = $('#message').val();

                if (!username) {
                    $('#formResult').html('<div style="color: #ff6b6b;">ユーザー名は必須です</div>');
                    return;
                }

                $('#formResult').html(`
                    <div style="color: #4ecdc4;">
                        <h4>送信されたデータ:</h4>
                        <p><strong>ユーザー名:</strong> ${username}</p>
                        <p><strong>メール:</strong> ${email || '未入力'}</p>
                        <p><strong>メッセージ:</strong> ${message || '未入力'}</p>
                    </div>
                `);
                logEvent('フォーム送信完了');
            });

            $('#clearForm').click(function() {
                $('#demoForm')[0].reset();
                $('#formResult').empty();
                logEvent('フォームクリア');
            });

            // ToDo リスト
            $('#addTask').click(function() {
                const taskText = $('#newTask').val().trim();
                if (taskText) {
                    const taskHtml = `
                        <div class="task-item">
                            <span>${taskText}</span>
                            <div>
                                <button class="button" onclick="$(this).parent().parent().toggleClass('completed')">完了</button>
                                <button class="button" onclick="$(this).parent().parent().remove()">削除</button>
                            </div>
                        </div>
                    `;
                    $('#taskList').append(taskHtml);
                    $('#newTask').val('');
                    logEvent(`タスク追加: ${taskText}`);
                }
            });

            $('#newTask').keypress(function(e) {
                if (e.which === 13) {
                    $('#addTask').click();
                }
            });

            // イメージギャラリー（イベント委任）
            $('.gallery').on('click', 'img', function() {
                const src = $(this).attr('src');
                const alt = $(this).attr('alt');
                $('#imageInfo').html(`選択された画像: ${alt} (${src})`);
                
                // 画像エフェクト
                $(this).effect || $(this).animate({opacity: 0.5}, 200).animate({opacity: 1}, 200);
                logEvent(`画像クリック: ${alt}`);
            });

            // Ajax通信
            $('#loadData').click(function() {
                $('#ajaxResult').html('<div class="loading">読み込み中...</div>');
                
                // JSONPlaceholder APIからデータを取得
                $.get('https://jsonplaceholder.typicode.com/posts/1')
                    .done(function(data) {
                        $('#ajaxResult').html(`
                            <h4>読み込み完了</h4>
                            <p><strong>タイトル:</strong> ${data.title}</p>
                            <p><strong>内容:</strong> ${data.body}</p>
                        `);
                        logEvent('Ajax通信成功');
                    })
                    .fail(function() {
                        $('#ajaxResult').html('<div style="color: #ff6b6b;">データの読み込みに失敗しました</div>');
                        logEvent('Ajax通信失敗');
                    });
            });

            $('#loadJSON').click(function() {
                $('#ajaxResult').html('<div class="loading">JSON読み込み中...</div>');
                
                $.getJSON('https://jsonplaceholder.typicode.com/users/1')
                    .done(function(user) {
                        $('#ajaxResult').html(`
                            <h4>ユーザー情報</h4>
                            <p><strong>名前:</strong> ${user.name}</p>
                            <p><strong>ユーザー名:</strong> ${user.username}</p>
                            <p><strong>メール:</strong> ${user.email}</p>
                            <p><strong>会社:</strong> ${user.company.name}</p>
                        `);
                        logEvent('JSON読み込み成功');
                    })
                    .fail(function() {
                        $('#ajaxResult').html('<div style="color: #ff6b6b;">JSONデータの読み込みに失敗しました</div>');
                        logEvent('JSON読み込み失敗');
                    });
            });

            // チェーンメソッドデモ
            $('#chainAnimation').click(function() {
                $('#chainDemo')
                    .fadeOut(500)
                    .delay(200)
                    .fadeIn(500)
                    .animate({width: '150px', height: '150px'}, 1000)
                    .animate({width: '100px', height: '100px'}, 1000);
                logEvent('チェーンアニメーション実行');
            });

            logEvent('jQueryデモページ初期化完了');
        });
    </script>
</body>
</html>
```

[^13]: jQuery: https://jquery.com/ - 世界最も使用されているJavaScriptライブラリ

### Alpine.js 3系 - Vue風の軽量フロントエンドフレームワーク

Alpine.js[^14]は、Vue.jsの宣言的な性質とjQueryの直接性を組み合わせた軽量フロントエンドフレームワークです。わずか15KBの軽量設計でありながら、リアクティブデータバインディング、コンポーネント、状態管理を提供します。

**特徴**:
- Vue.js風の宣言的構文
- 軽量設計（15KB gzipped）
- ビルドプロセス不要
- リアクティブデータバインディング
- コンポーネント指向

**信頼性スコア**: 8/10（Vue風記法・軽量）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alpine.js デモ</title>
    <script src="https://unpkg.com/alpinejs@3.14.1/dist/cdn.min.js" defer></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: white;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        .demo-section {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 25px;
            margin: 25px 0;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .btn {
            background: #4ecdc4;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            margin: 5px;
            transition: all 0.3s ease;
            font-size: 14px;
            font-weight: 500;
        }
        .btn:hover {
            background: #45b7aa;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }
        .btn-secondary {
            background: #95a5a6;
        }
        .btn-secondary:hover {
            background: #7f8c8d;
        }
        .btn-danger {
            background: #e74c3c;
        }
        .btn-danger:hover {
            background: #c0392b;
        }
        .input {
            padding: 10px;
            border: none;
            border-radius: 8px;
            background: rgba(255, 255, 255, 0.9);
            color: #333;
            margin: 5px;
            font-size: 14px;
        }
        .card {
            background: rgba(255, 255, 255, 0.15);
            border-radius: 12px;
            padding: 20px;
            margin: 15px 0;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }
        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }
        .product-card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            transition: transform 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .product-card:hover {
            transform: translateY(-5px);
        }
        .tab {
            background: rgba(255, 255, 255, 0.1);
            border: none;
            color: white;
            padding: 10px 20px;
            cursor: pointer;
            border-radius: 8px 8px 0 0;
            margin-right: 5px;
        }
        .tab.active {
            background: rgba(255, 255, 255, 0.3);
        }
        .tab-content {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 0 8px 8px 8px;
            min-height: 150px;
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        .modal-content {
            background: white;
            color: #333;
            padding: 30px;
            border-radius: 15px;
            max-width: 500px;
            width: 90%;
            position: relative;
        }
        .close {
            position: absolute;
            top: 10px;
            right: 15px;
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #999;
        }
        .progress-bar {
            background: rgba(255, 255, 255, 0.3);
            border-radius: 10px;
            overflow: hidden;
            height: 20px;
            margin: 10px 0;
        }
        .progress-fill {
            background: #4ecdc4;
            height: 100%;
            transition: width 0.3s ease;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Alpine.js 3.14 デモページ</h1>
        <p>Vue.js風の宣言的構文とjQueryの直接性を組み合わせた軽量フレームワーク</p>

        <div class="grid">
            <!-- 基本的なリアクティビティ -->
            <div class="demo-section">
                <h2>リアクティブカウンター</h2>
                <div x-data="{ count: 0 }" class="card">
                    <h3>カウント: <span x-text="count"></span></h3>
                    <button class="btn" @click="count++">+1</button>
                    <button class="btn" @click="count--">-1</button>
                    <button class="btn btn-secondary" @click="count = 0">リセット</button>
                    
                    <div style="margin-top: 15px;">
                        <div x-show="count > 0" style="color: #4ecdc4;">
                            ✅ カウントが正の数です
                        </div>
                        <div x-show="count < 0" style="color: #ff6b6b;">
                            ⚠️ カウントが負の数です
                        </div>
                        <div x-show="count === 0" style="color: #95a5a6;">
                            ⭕ カウントがゼロです
                        </div>
                    </div>
                </div>
            </div>

            <!-- フォーム入力とバインディング -->
            <div class="demo-section">
                <h2>フォームデータバインディング</h2>
                <div x-data="{ name: '', email: '', message: '' }" class="card">
                    <input 
                        x-model="name" 
                        placeholder="お名前" 
                        class="input" 
                        style="width: 100%; margin-bottom: 10px;"
                    >
                    <input 
                        x-model="email" 
                        type="email" 
                        placeholder="メールアドレス" 
                        class="input" 
                        style="width: 100%; margin-bottom: 10px;"
                    >
                    <textarea 
                        x-model="message" 
                        placeholder="メッセージ" 
                        class="input" 
                        style="width: 100%; margin-bottom: 15px; min-height: 80px;"
                    ></textarea>
                    
                    <div style="background: rgba(0,0,0,0.2); padding: 15px; border-radius: 8px;">
                        <h4>プレビュー:</h4>
                        <p><strong>名前:</strong> <span x-text="name || '未入力'"></span></p>
                        <p><strong>メール:</strong> <span x-text="email || '未入力'"></span></p>
                        <p><strong>メッセージ:</strong> <span x-text="message || '未入力'"></span></p>
                    </div>
                </div>
            </div>
        </div>

        <!-- タブシステム -->
        <div class="demo-section">
            <h2>動的タブシステム</h2>
            <div x-data="{ activeTab: 'profile' }">
                <div>
                    <button class="tab" :class="{ active: activeTab === 'profile' }" @click="activeTab = 'profile'">
                        プロフィール
                    </button>
                    <button class="tab" :class="{ active: activeTab === 'settings' }" @click="activeTab = 'settings'">
                        設定
                    </button>
                    <button class="tab" :class="{ active: activeTab === 'about' }" @click="activeTab = 'about'">
                        について
                    </button>
                </div>
                
                <div class="tab-content">
                    <div x-show="activeTab === 'profile'" x-transition>
                        <h3>プロフィール</h3>
                        <p>ユーザーのプロフィール情報をここに表示します。アバター、自己紹介、連絡先などの情報を管理できます。</p>
                        <button class="btn">プロフィール編集</button>
                    </div>
                    
                    <div x-show="activeTab === 'settings'" x-transition>
                        <h3>設定</h3>
                        <p>アプリケーションの各種設定を行います。通知設定、プライバシー設定、アカウント設定などを変更できます。</p>
                        <button class="btn">設定を保存</button>
                    </div>
                    
                    <div x-show="activeTab === 'about'" x-transition>
                        <h3>について</h3>
                        <p>このアプリケーションについての情報です。バージョン情報、ライセンス、お問い合わせ先などを確認できます。</p>
                        <button class="btn">サポートに連絡</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- ショッピングカート例 -->
        <div class="demo-section">
            <h2>ショッピングカート（状態管理）</h2>
            <div x-data="{
                products: [
                    { id: 1, name: 'ノートPC', price: 89000, image: '💻' },
                    { id: 2, name: 'スマートフォン', price: 65000, image: '📱' },
                    { id: 3, name: 'ヘッドフォン', price: 12000, image: '🎧' },
                    { id: 4, name: 'マウス', price: 3500, image: '🖱️' }
                ],
                cart: [],
                addToCart(product) {
                    const existingItem = this.cart.find(item => item.id === product.id);
                    if (existingItem) {
                        existingItem.quantity++;
                    } else {
                        this.cart.push({...product, quantity: 1});
                    }
                },
                removeFromCart(productId) {
                    const index = this.cart.findIndex(item => item.id === productId);
                    if (index > -1) {
                        if (this.cart[index].quantity > 1) {
                            this.cart[index].quantity--;
                        } else {
                            this.cart.splice(index, 1);
                        }
                    }
                },
                get totalPrice() {
                    return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0);
                },
                get totalItems() {
                    return this.cart.reduce((total, item) => total + item.quantity, 0);
                }
            }">
                <div style="display: grid; grid-template-columns: 2fr 1fr; gap: 30px;">
                    <div>
                        <h3>商品一覧</h3>
                        <div class="product-grid">
                            <template x-for="product in products" :key="product.id">
                                <div class="product-card">
                                    <div style="font-size: 3rem; margin-bottom: 10px;" x-text="product.image"></div>
                                    <h4 x-text="product.name"></h4>
                                    <p style="font-size: 1.2rem; font-weight: bold; color: #4ecdc4;">
                                        ¥<span x-text="product.price.toLocaleString()"></span>
                                    </p>
                                    <button class="btn" @click="addToCart(product)">
                                        カートに追加
                                    </button>
                                </div>
                            </template>
                        </div>
                    </div>
                    
                    <div>
                        <h3>ショッピングカート (<span x-text="totalItems"></span>)</h3>
                        <div class="card">
                            <template x-for="item in cart" :key="item.id">
                                <div style="display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid rgba(255,255,255,0.2);">
                                    <div>
                                        <span x-text="item.name"></span>
                                        <div style="font-size: 0.9rem; opacity: 0.8;">
                                            ¥<span x-text="item.price.toLocaleString()"></span> × <span x-text="item.quantity"></span>
                                        </div>
                                    </div>
                                    <div>
                                        <button class="btn" style="padding: 5px 10px; font-size: 12px;" @click="addToCart(item)">+</button>
                                        <button class="btn btn-danger" style="padding: 5px 10px; font-size: 12px;" @click="removeFromCart(item.id)">-</button>
                                    </div>
                                </div>
                            </template>
                            
                            <div x-show="cart.length === 0" style="text-align: center; padding: 20px; opacity: 0.6;">
                                カートは空です
                            </div>
                            
                            <div x-show="cart.length > 0" style="margin-top: 15px; padding-top: 15px; border-top: 2px solid rgba(255,255,255,0.3);">
                                <div style="display: flex; justify-content: space-between; font-size: 1.2rem; font-weight: bold;">
                                    <span>合計:</span>
                                    <span style="color: #4ecdc4;">¥<span x-text="totalPrice.toLocaleString()"></span></span>
                                </div>
                                <button class="btn" style="width: 100%; margin-top: 15px;">
                                    購入手続きへ
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- モーダルダイアログ -->
        <div class="demo-section">
            <h2>モーダルダイアログ</h2>
            <div x-data="{ showModal: false }">
                <button class="btn" @click="showModal = true">
                    モーダルを開く
                </button>
                
                <div x-show="showModal" x-transition class="modal" @click.self="showModal = false">
                    <div class="modal-content">
                        <button class="close" @click="showModal = false">&times;</button>
                        <h3>Alpine.js モーダル</h3>
                        <p>これはAlpine.jsで作成されたモーダルダイアログです。x-showディレクティブとx-transitionを使用してスムーズな表示/非表示を実現しています。</p>
                        <div style="margin-top: 20px;">
                            <button class="btn" @click="showModal = false">閉じる</button>
                            <button class="btn btn-secondary" style="margin-left: 10px;">キャンセル</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- アニメーションとトランジション -->
        <div class="demo-section">
            <h2>アニメーションとトランジション</h2>
            <div x-data="{ 
                show: true, 
                progress: 0,
                startProgress() {
                    this.progress = 0;
                    const interval = setInterval(() => {
                        this.progress += 5;
                        if (this.progress >= 100) {
                            clearInterval(interval);
                        }
                    }, 100);
                }
            }">
                <button class="btn" @click="show = !show">
                    要素を<span x-text="show ? '非表示' : '表示'"></span>
                </button>
                <button class="btn btn-secondary" @click="startProgress()">
                    プログレス開始
                </button>
                
                <div x-show="show" 
                     x-transition:enter="transition ease-out duration-300"
                     x-transition:enter-start="opacity-0 transform scale-90"
                     x-transition:enter-end="opacity-100 transform scale-100"
                     x-transition:leave="transition ease-in duration-300"
                     x-transition:leave-start="opacity-100 transform scale-100"
                     x-transition:leave-end="opacity-0 transform scale-90"
                     class="card" 
                     style="margin-top: 20px;">
                    <h4>🎨 アニメーション要素</h4>
                    <p>この要素はx-transitionディレクティブを使用してスムーズにアニメーションします。</p>
                </div>
                
                <div style="margin-top: 20px;">
                    <h4>プログレスバー: <span x-text="progress"></span>%</h4>
                    <div class="progress-bar">
                        <div class="progress-fill" :style="`width: ${progress}%`"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
```

[^14]: Alpine.js: https://alpinejs.dev/ - 軽量リアクティブフロントエンドフレームワーク

### GSAP 3.13.0 - 高性能アニメーションライブラリ

GSAP（GreenSock Animation Platform）[^15]は、業界標準の高性能JavaScriptアニメーションライブラリです。Adobe、Google、Microsoft等の大手企業で採用されており、60FPSのスムーズなアニメーションを実現します。

**特徴**:
- 高性能なタイムライン制御
- CSS、SVG、Canvas対応
- プラグインアーキテクチャ
- モーフィング、パス描画等の高度な機能
- 逆再生、一時停止、スピード制御

**信頼性スコア**: 10/10（業界標準・高性能）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GSAP デモ</title>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/TextPlugin.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            overflow-x: hidden;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
        }
        .demo-section {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 50px 0;
        }
        .animate-box {
            width: 100px;
            height: 100px;
            background: #4ecdc4;
            border-radius: 10px;
            margin: 20px;
            cursor: pointer;
        }
        .btn {
            background: #4ecdc4;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            margin: 10px;
            font-size: 16px;
            transition: background 0.3s ease;
        }
        .btn:hover {
            background: #45b7aa;
        }
        .card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
            margin: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .progress-container {
            width: 100%;
            height: 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
        }
        .progress-bar {
            height: 100%;
            background: #4ecdc4;
            width: 0%;
            border-radius: 10px;
        }
        .text-container {
            font-size: 2rem;
            margin: 30px 0;
            min-height: 100px;
        }
        .morph-container {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 40px 0;
        }
        .morph-shape {
            width: 200px;
            height: 200px;
        }
        .timeline-demo {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
            margin: 30px 0;
        }
        .timeline-box {
            width: 80px;
            height: 80px;
            background: #ff6b6b;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 18px;
        }
        .scroll-section {
            height: 200vh;
            position: relative;
        }
        .scroll-element {
            position: absolute;
            width: 100px;
            height: 100px;
            background: #feca57;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
        }
    </style>
</head>
<body>
    <!-- ヒーローセクション -->
    <div class="hero">
        <div>
            <h1 id="title">GSAP 3.13.0 デモ</h1>
            <p id="subtitle">業界標準の高性能アニメーションライブラリ</p>
            <button class="btn" onclick="startHeroAnimation()">アニメーション開始</button>
        </div>
    </div>

    <div class="container">
        <!-- 基本アニメーション -->
        <div class="demo-section">
            <div class="card">
                <h2>基本アニメーション</h2>
                <div style="display: flex; flex-wrap: wrap; justify-content: center;">
                    <div class="animate-box" id="box1"></div>
                    <div class="animate-box" id="box2"></div>
                    <div class="animate-box" id="box3"></div>
                    <div class="animate-box" id="box4"></div>
                </div>
                <div style="text-align: center;">
                    <button class="btn" onclick="animateBoxes()">回転アニメーション</button>
                    <button class="btn" onclick="bounceBoxes()">バウンスアニメーション</button>
                    <button class="btn" onclick="morphBoxes()">モーフィング</button>
                    <button class="btn" onclick="resetBoxes()">リセット</button>
                </div>
            </div>
        </div>

        <!-- タイムラインアニメーション -->
        <div class="demo-section">
            <div class="card">
                <h2>タイムラインアニメーション</h2>
                <div class="timeline-demo">
                    <div class="timeline-box" id="tl1">1</div>
                    <div class="timeline-box" id="tl2">2</div>
                    <div class="timeline-box" id="tl3">3</div>
                    <div class="timeline-box" id="tl4">4</div>
                    <div class="timeline-box" id="tl5">5</div>
                </div>
                <div style="text-align: center;">
                    <button class="btn" onclick="playTimeline()">タイムライン再生</button>
                    <button class="btn" onclick="reverseTimeline()">逆再生</button>
                    <button class="btn" onclick="pauseTimeline()">一時停止</button>
                    <button class="btn" onclick="restartTimeline()">再開</button>
                </div>
                <div class="progress-container">
                    <div class="progress-bar" id="timelineProgress"></div>
                </div>
            </div>
        </div>

        <!-- テキストアニメーション -->
        <div class="demo-section">
            <div class="card">
                <h2>テキストアニメーション</h2>
                <div class="text-container" id="textDemo">
                    ここにアニメーションテキストが表示されます
                </div>
                <div style="text-align: center;">
                    <button class="btn" onclick="typewriterEffect()">タイプライター効果</button>
                    <button class="btn" onclick="splitTextAnimation()">文字分割アニメーション</button>
                    <button class="btn" onclick="morphTextAnimation()">テキストモーフィング</button>
                </div>
            </div>
        </div>

        <!-- SVGアニメーション -->
        <div class="demo-section">
            <div class="card">
                <h2>SVGアニメーション</h2>
                <div class="morph-container">
                    <svg class="morph-shape" viewBox="0 0 200 200">
                        <path id="morphPath" d="M100,50 L150,100 L100,150 L50,100 Z" 
                              fill="#4ecdc4" stroke="white" stroke-width="3"/>
                    </svg>
                </div>
                <div style="text-align: center;">
                    <button class="btn" onclick="morphToCircle()">円に変形</button>
                    <button class="btn" onclick="morphToStar()">星に変形</button>
                    <button class="btn" onclick="morphToHeart()">ハートに変形</button>
                    <button class="btn" onclick="morphToSquare()">四角に戻す</button>
                </div>
                <div style="margin-top: 30px; text-align: center;">
                    <svg width="300" height="100" id="drawingPath">
                        <path id="drawPath" d="M50,50 Q150,10 250,50" 
                              stroke="#feca57" stroke-width="4" fill="none" 
                              stroke-dasharray="200" stroke-dashoffset="200"/>
                    </svg>
                    <br>
                    <button class="btn" onclick="drawPath()">パス描画</button>
                </div>
            </div>
        </div>

        <!-- スクロールトリガー -->
        <div class="scroll-section" id="scrollSection">
            <div class="card" style="position: sticky; top: 50px; z-index: 10;">
                <h2>スクロールトリガーアニメーション</h2>
                <p>このセクションをスクロールして、要素が動く様子を確認してください。</p>
            </div>
            
            <div class="scroll-element" id="scrollEl1" style="top: 300px; left: 10%;">🚀</div>
            <div class="scroll-element" id="scrollEl2" style="top: 600px; right: 10%;">⭐</div>
            <div class="scroll-element" id="scrollEl3" style="top: 900px; left: 50%;">🎯</div>
            <div class="scroll-element" id="scrollEl4" style="top: 1200px; right: 30%;">💎</div>
        </div>

        <!-- 3Dアニメーション -->
        <div class="demo-section">
            <div class="card">
                <h2>3D変形アニメーション</h2>
                <div style="perspective: 1000px; display: flex; justify-content: center; align-items: center; height: 300px;">
                    <div id="cube3d" style="
                        width: 150px;
                        height: 150px;
                        background: linear-gradient(45deg, #4ecdc4, #44a08d);
                        border-radius: 10px;
                        display: flex;
                        align-items: center;
                        justify-content: center;
                        font-size: 24px;
                        font-weight: bold;
                        cursor: pointer;
                        transform-style: preserve-3d;
                    ">3D CUBE</div>
                </div>
                <div style="text-align: center;">
                    <button class="btn" onclick="rotate3D()">3D回転</button>
                    <button class="btn" onclick="flip3D()">3Dフリップ</button>
                    <button class="btn" onclick="perspective3D()">パースペクティブ</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // GSAP登録
        gsap.registerPlugin(ScrollTrigger, TextPlugin);

        // グローバル変数
        let mainTimeline;

        // ヒーローアニメーション
        function startHeroAnimation() {
            gsap.fromTo('#title', 
                { y: -100, opacity: 0 },
                { y: 0, opacity: 1, duration: 1, ease: 'bounce.out' }
            );
            gsap.fromTo('#subtitle',
                { y: 100, opacity: 0 },
                { y: 0, opacity: 1, duration: 1, delay: 0.5, ease: 'power2.out' }
            );
        }

        // 基本アニメーション
        function animateBoxes() {
            gsap.to('.animate-box', {
                rotation: 360,
                duration: 1,
                stagger: 0.1,
                ease: 'power2.inOut'
            });
        }

        function bounceBoxes() {
            gsap.to('.animate-box', {
                y: -50,
                duration: 0.5,
                yoyo: true,
                repeat: 1,
                stagger: 0.1,
                ease: 'bounce.out'
            });
        }

        function morphBoxes() {
            gsap.to('.animate-box', {
                borderRadius: '50%',
                scale: 1.2,
                backgroundColor: '#ff6b6b',
                duration: 0.8,
                stagger: 0.1,
                yoyo: true,
                repeat: 1,
                ease: 'elastic.out(1, 0.3)'
            });
        }

        function resetBoxes() {
            gsap.set('.animate-box', {
                rotation: 0,
                y: 0,
                scale: 1,
                borderRadius: '10px',
                backgroundColor: '#4ecdc4'
            });
        }

        // タイムラインアニメーション
        function createMainTimeline() {
            mainTimeline = gsap.timeline({ paused: true, onUpdate: updateProgress });
            
            mainTimeline
                .to('#tl1', { scale: 1.5, backgroundColor: '#4ecdc4', duration: 0.5 })
                .to('#tl2', { scale: 1.5, backgroundColor: '#4ecdc4', duration: 0.5 }, '-=0.3')
                .to('#tl3', { scale: 1.5, backgroundColor: '#4ecdc4', duration: 0.5 }, '-=0.3')
                .to('#tl4', { scale: 1.5, backgroundColor: '#4ecdc4', duration: 0.5 }, '-=0.3')
                .to('#tl5', { scale: 1.5, backgroundColor: '#4ecdc4', duration: 0.5 }, '-=0.3')
                .to('.timeline-box', { 
                    y: -30, 
                    rotation: 720,
                    duration: 1,
                    stagger: 0.1,
                    ease: 'power2.inOut'
                })
                .to('.timeline-box', {
                    scale: 1,
                    y: 0,
                    rotation: 0,
                    backgroundColor: '#ff6b6b',
                    duration: 0.8,
                    stagger: 0.1
                });
        }

        function updateProgress() {
            const progress = mainTimeline.progress() * 100;
            gsap.set('#timelineProgress', { width: progress + '%' });
        }

        function playTimeline() {
            if (!mainTimeline) createMainTimeline();
            mainTimeline.play();
        }

        function reverseTimeline() {
            if (!mainTimeline) createMainTimeline();
            mainTimeline.reverse();
        }

        function pauseTimeline() {
            if (mainTimeline) mainTimeline.pause();
        }

        function restartTimeline() {
            if (mainTimeline) mainTimeline.resume();
        }

        // テキストアニメーション
        function typewriterEffect() {
            gsap.to('#textDemo', {
                text: 'GSAPのテキストプラグインを使用したタイプライター効果です。一文字ずつアニメーションしながら表示されます。',
                duration: 3,
                ease: 'none'
            });
        }

        function splitTextAnimation() {
            const text = 'Split Text Animation';
            document.getElementById('textDemo').innerHTML = text.split('').map(char => 
                char === ' ' ? ' ' : `<span style="display: inline-block;">${char}</span>`
            ).join('');
            
            gsap.fromTo('#textDemo span', 
                { y: 100, opacity: 0, rotationX: -90 },
                { 
                    y: 0, 
                    opacity: 1, 
                    rotationX: 0,
                    duration: 0.8,
                    stagger: 0.05,
                    ease: 'back.out(1.7)'
                }
            );
        }

        function morphTextAnimation() {
            const texts = [
                'GSAP is Awesome!',
                'High Performance',
                'Cross Browser',
                'Easy to Use',
                'Industry Standard'
            ];
            let currentIndex = 0;
            
            function morphNext() {
                gsap.to('#textDemo', {
                    scale: 0.8,
                    opacity: 0,
                    duration: 0.3,
                    onComplete: () => {
                        currentIndex = (currentIndex + 1) % texts.length;
                        document.getElementById('textDemo').textContent = texts[currentIndex];
                        gsap.to('#textDemo', {
                            scale: 1,
                            opacity: 1,
                            duration: 0.3
                        });
                    }
                });
                
                if (currentIndex < texts.length - 1 || currentIndex === texts.length - 1) {
                    setTimeout(morphNext, 1500);
                }
            }
            
            morphNext();
        }

        // SVGアニメーション
        function morphToCircle() {
            gsap.to('#morphPath', {
                attr: { d: 'M100,20 A80,80 0 1,1 99.9,20 Z' },
                duration: 1,
                ease: 'power2.inOut'
            });
        }

        function morphToStar() {
            gsap.to('#morphPath', {
                attr: { d: 'M100,20 L110,60 L150,60 L120,90 L130,130 L100,110 L70,130 L80,90 L50,60 L90,60 Z' },
                duration: 1,
                ease: 'power2.inOut'
            });
        }

        function morphToHeart() {
            gsap.to('#morphPath', {
                attr: { d: 'M100,160 C100,160 60,120 60,90 C60,70 75,55 95,55 C100,55 100,55 100,55 C100,55 100,55 105,55 C125,55 140,70 140,90 C140,120 100,160 100,160 Z' },
                duration: 1,
                ease: 'power2.inOut'
            });
        }

        function morphToSquare() {
            gsap.to('#morphPath', {
                attr: { d: 'M100,50 L150,100 L100,150 L50,100 Z' },
                duration: 1,
                ease: 'power2.inOut'
            });
        }

        function drawPath() {
            gsap.fromTo('#drawPath', 
                { strokeDashoffset: 200 },
                { 
                    strokeDashoffset: 0,
                    duration: 2,
                    ease: 'power2.inOut'
                }
            );
        }

        // 3Dアニメーション
        function rotate3D() {
            gsap.to('#cube3d', {
                rotationY: 360,
                rotationX: 360,
                duration: 2,
                ease: 'power2.inOut'
            });
        }

        function flip3D() {
            gsap.to('#cube3d', {
                rotationY: 180,
                duration: 1,
                yoyo: true,
                repeat: 1,
                ease: 'power2.inOut'
            });
        }

        function perspective3D() {
            gsap.to('#cube3d', {
                z: 200,
                rotationY: 45,
                rotationX: 30,
                duration: 1,
                yoyo: true,
                repeat: 1,
                ease: 'power2.inOut'
            });
        }

        // スクロールトリガー初期化
        gsap.registerPlugin(ScrollTrigger);

        // スクロール要素のアニメーション
        gsap.utils.toArray('.scroll-element').forEach((element, index) => {
            gsap.fromTo(element, 
                {
                    x: index % 2 === 0 ? -200 : 200,
                    opacity: 0,
                    rotation: -180
                },
                {
                    x: 0,
                    opacity: 1,
                    rotation: 0,
                    duration: 1,
                    ease: 'power2.out',
                    scrollTrigger: {
                        trigger: element,
                        start: 'top 80%',
                        end: 'bottom 20%',
                        toggleActions: 'play none none reverse'
                    }
                }
            );
        });

        // 初期アニメーション
        window.addEventListener('load', () => {
            startHeroAnimation();
        });
    </script>
</body>
</html>
```

[^15]: GSAP: https://gsap.com/ - 業界標準の高性能JavaScriptアニメーションライブラリ

### AOS 2.3.4 - スクロール連動アニメーション

AOS（Animate On Scroll）[^16]は、スクロール位置に応じて要素をアニメーションさせる軽量ライブラリです。Intersection Observer API[^17]を活用し、パフォーマンスに配慮した実装が特徴です。

**特徴**:
- スクロール連動アニメーション特化
- 60種類以上のアニメーション効果
- レスポンシブ対応
- 軽量設計（4KB gzipped）
- 設定の柔軟性

**信頼性スコア**: 8/10（スクロール特化・軽量）

**デモコード**:
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AOS デモ</title>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(180deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            color: white;
        }
        .section {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 50px 20px;
        }
        .container {
            max-width: 1200px;
            width: 100%;
        }
        .hero {
            text-align: center;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 20px;
            padding: 60px;
        }
        .card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
            margin: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin: 50px 0;
        }
        .feature-box {
            background: rgba(255, 255, 255, 0.15);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .icon {
            font-size: 4rem;
            margin-bottom: 20px;
            display: block;
        }
        .timeline {
            position: relative;
            max-width: 800px;
            margin: 0 auto;
        }
        .timeline::after {
            content: '';
            position: absolute;
            width: 4px;
            background: rgba(255, 255, 255, 0.3);
            top: 0;
            bottom: 0;
            left: 50%;
            margin-left: -2px;
        }
        .timeline-item {
            padding: 20px 40px;
            position: relative;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            margin: 30px 0;
            width: calc(50% - 40px);
        }
        .timeline-item.left {
            left: 0;
        }
        .timeline-item.right {
            left: 50%;
        }
        .timeline-item::after {
            content: '';
            position: absolute;
            width: 20px;
            height: 20px;
            background: #4ecdc4;
            border: 4px solid white;
            top: 50%;
            border-radius: 50%;
            z-index: 1;
        }
        .timeline-item.left::after {
            right: -30px;
        }
        .timeline-item.right::after {
            left: -30px;
        }
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 50px 0;
        }
        .gallery-item {
            height: 200px;
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            margin: 50px 0;
        }
        .stat-item {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
        }
        .stat-number {
            font-size: 3rem;
            font-weight: bold;
            color: #4ecdc4;
            margin-bottom: 10px;
        }
        .floating-elements {
            position: relative;
            height: 400px;
            overflow: hidden;
        }
        .floating-item {
            position: absolute;
            width: 60px;
            height: 60px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
        }
        @media (max-width: 768px) {
            .timeline::after {
                left: 20px;
            }
            .timeline-item {
                width: calc(100% - 80px);
                left: 40px !important;
            }
            .timeline-item::after {
                left: -30px !important;
            }
        }
    </style>
</head>
<body>
    <!-- ヒーローセクション -->
    <div class="section">
        <div class="container">
            <div class="hero">
                <h1 data-aos="fade-up" data-aos-duration="1000">AOS Library Demo</h1>
                <p data-aos="fade-up" data-aos-delay="200" data-aos-duration="1000">
                    スクロールに連動した美しいアニメーション効果
                </p>
                <div data-aos="zoom-in" data-aos-delay="400" data-aos-duration="800">
                    <button style="
                        background: #4ecdc4;
                        color: white;
                        border: none;
                        padding: 15px 30px;
                        border-radius: 25px;
                        font-size: 18px;
                        cursor: pointer;
                        margin-top: 20px;
                    ">スクロールして体験</button>
                </div>
            </div>
        </div>
    </div>

    <!-- 機能紹介セクション -->
    <div class="section">
        <div class="container">
            <h2 data-aos="fade-right" style="text-align: center; margin-bottom: 50px; font-size: 2.5rem;">
                主な機能
            </h2>
            <div class="grid">
                <div class="feature-box" data-aos="flip-left" data-aos-delay="100">
                    <span class="icon">🎯</span>
                    <h3>簡単設定</h3>
                    <p>data属性を追加するだけでアニメーションを実装できます。複雑な設定は不要です。</p>
                </div>
                <div class="feature-box" data-aos="flip-left" data-aos-delay="200">
                    <span class="icon">⚡</span>
                    <h3>高性能</h3>
                    <p>Intersection Observer APIを使用し、スクロールパフォーマンスを最適化しています。</p>
                </div>
                <div class="feature-box" data-aos="flip-left" data-aos-delay="300">
                    <span class="icon">📱</span>
                    <h3>レスポンシブ</h3>
                    <p>デバイスサイズに応じてアニメーションを無効化する機能を提供します。</p>
                </div>
            </div>
        </div>
    </div>

    <!-- アニメーション種類デモ -->
    <div class="section">
        <div class="container">
            <h2 data-aos="fade-up" style="text-align: center; margin-bottom: 50px;">
                様々なアニメーション効果
            </h2>
            
            <!-- フェード系 -->
            <div style="margin: 80px 0;">
                <h3 data-aos="slide-right">フェード系アニメーション</h3>
                <div class="grid">
                    <div class="card" data-aos="fade-up">
                        <h4>Fade Up</h4>
                        <p>下から上にフェードイン</p>
                    </div>
                    <div class="card" data-aos="fade-down">
                        <h4>Fade Down</h4>
                        <p>上から下にフェードイン</p>
                    </div>
                    <div class="card" data-aos="fade-left">
                        <h4>Fade Left</h4>
                        <p>右から左にフェードイン</p>
                    </div>
                    <div class="card" data-aos="fade-right">
                        <h4>Fade Right</h4>
                        <p>左から右にフェードイン</p>
                    </div>
                </div>
            </div>

            <!-- スライド系 -->
            <div style="margin: 80px 0;">
                <h3 data-aos="slide-left">スライド系アニメーション</h3>
                <div class="grid">
                    <div class="card" data-aos="slide-up" data-aos-duration="800">
                        <h4>Slide Up</h4>
                        <p>下からスライドイン</p>
                    </div>
                    <div class="card" data-aos="slide-down" data-aos-duration="800">
                        <h4>Slide Down</h4>
                        <p>上からスライドイン</p>
                    </div>
                    <div class="card" data-aos="slide-left" data-aos-duration="800">
                        <h4>Slide Left</h4>
                        <p>右からスライドイン</p>
                    </div>
                    <div class="card" data-aos="slide-right" data-aos-duration="800">
                        <h4>Slide Right</h4>
                        <p>左からスライドイン</p>
                    </div>
                </div>
            </div>

            <!-- ズーム・回転系 -->
            <div style="margin: 80px 0;">
                <h3 data-aos="zoom-in">ズーム・回転系アニメーション</h3>
                <div class="grid">
                    <div class="card" data-aos="zoom-in" data-aos-delay="100">
                        <h4>Zoom In</h4>
                        <p>中心から拡大</p>
                    </div>
                    <div class="card" data-aos="zoom-out" data-aos-delay="200">
                        <h4>Zoom Out</h4>
                        <p>大きい状態から縮小</p>
                    </div>
                    <div class="card" data-aos="flip-up" data-aos-delay="300">
                        <h4>Flip Up</h4>
                        <p>上方向に回転</p>
                    </div>
                    <div class="card" data-aos="flip-down" data-aos-delay="400">
                        <h4>Flip Down</h4>
                        <p>下方向に回転</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- タイムライン -->
    <div class="section">
        <div class="container">
            <h2 data-aos="fade-up" style="text-align: center; margin-bottom: 50px;">
                開発タイムライン
            </h2>
            <div class="timeline">
                <div class="timeline-item left" data-aos="fade-right" data-aos-delay="100">
                    <h4>2015年</h4>
                    <p>プロジェクト開始。シンプルなスクロールアニメーションライブラリとして誕生。</p>
                </div>
                <div class="timeline-item right" data-aos="fade-left" data-aos-delay="200">
                    <h4>2017年</h4>
                    <p>Intersection Observer API対応により、パフォーマンスが大幅に向上。</p>
                </div>
                <div class="timeline-item left" data-aos="fade-right" data-aos-delay="300">
                    <h4>2019年</h4>
                    <p>レスポンシブ対応と詳細な設定オプションを追加。</p>
                </div>
                <div class="timeline-item right" data-aos="fade-left" data-aos-delay="400">
                    <h4>2021年</h4>
                    <p>TypeScript定義ファイル提供開始。モダンな開発環境をサポート。</p>
                </div>
                <div class="timeline-item left" data-aos="fade-right" data-aos-delay="500">
                    <h4>2023年</h4>
                    <p>最新ブラウザ対応とパフォーマンス最適化を継続的に実施。</p>
                </div>
            </div>
        </div>
    </div>

    <!-- 統計情報 -->
    <div class="section">
        <div class="container">
            <h2 data-aos="fade-up" style="text-align: center; margin-bottom: 50px;">
                プロジェクト統計
            </h2>
            <div class="stats">
                <div class="stat-item" data-aos="count-up" data-aos-delay="100">
                    <div class="stat-number" data-target="50000">0</div>
                    <h4>GitHub Stars</h4>
                </div>
                <div class="stat-item" data-aos="count-up" data-aos-delay="200">
                    <div class="stat-number" data-target="2000000">0</div>
                    <h4>Weekly Downloads</h4>
                </div>
                <div class="stat-item" data-aos="count-up" data-aos-delay="300">
                    <div class="stat-number" data-target="60">0</div>
                    <h4>Animation Types</h4>
                </div>
                <div class="stat-item" data-aos="count-up" data-aos-delay="400">
                    <div class="stat-number" data-target="98">0</div>
                    <h4>Browser Support %</h4>
                </div>
            </div>
        </div>
    </div>

    <!-- ギャラリー -->
    <div class="section">
        <div class="container">
            <h2 data-aos="fade-up" style="text-align: center; margin-bottom: 50px;">
                インタラクティブギャラリー
            </h2>
            <div class="gallery">
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="100">🎨</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="200">🚀</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="300">⭐</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="400">🎯</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="500">💎</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="600">🔥</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="700">⚡</div>
                <div class="gallery-item" data-aos="zoom-in-up" data-aos-delay="800">🌟</div>
            </div>
        </div>
    </div>

    <!-- フローティング要素 -->
    <div class="section">
        <div class="container">
            <h2 data-aos="fade-up" style="text-align: center; margin-bottom: 50px;">
                複雑なアニメーション組み合わせ
            </h2>
            <div class="floating-elements">
                <div class="floating-item" 
                     style="top: 10%; left: 10%;" 
                     data-aos="fade-up" 
                     data-aos-delay="100"
                     data-aos-duration="1000">🌸</div>
                <div class="floating-item" 
                     style="top: 20%; right: 15%;" 
                     data-aos="fade-down" 
                     data-aos-delay="200"
                     data-aos-duration="1200">🦋</div>
                <div class="floating-item" 
                     style="top: 50%; left: 20%;" 
                     data-aos="fade-right" 
                     data-aos-delay="300"
                     data-aos-duration="1400">🌿</div>
                <div class="floating-item" 
                     style="top: 60%; right: 25%;" 
                     data-aos="fade-left" 
                     data-aos-delay="400"
                     data-aos-duration="1600">🌺</div>
                <div class="floating-item" 
                     style="bottom: 20%; left: 50%;" 
                     data-aos="zoom-in" 
                     data-aos-delay="500"
                     data-aos-duration="1800">🍀</div>
            </div>
        </div>
    </div>

    <!-- 最終セクション -->
    <div class="section">
        <div class="container">
            <div class="hero">
                <h2 data-aos="flip-up" data-aos-duration="1000">AOSで素晴らしい体験を</h2>
                <p data-aos="fade-up" data-aos-delay="200" data-aos-duration="1000">
                    シンプルな設定で、印象的なスクロールアニメーションを実現しましょう
                </p>
                <div data-aos="fade-up" data-aos-delay="400" data-aos-duration="1000">
                    <button style="
                        background: #4ecdc4;
                        color: white;
                        border: none;
                        padding: 15px 30px;
                        border-radius: 25px;
                        font-size: 18px;
                        cursor: pointer;
                        margin: 10px;
                    ">公式サイトへ</button>
                    <button style="
                        background: transparent;
                        color: white;
                        border: 2px solid white;
                        padding: 15px 30px;
                        border-radius: 25px;
                        font-size: 18px;
                        cursor: pointer;
                        margin: 10px;
                    ">GitHub</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script>
        // AOS初期化
        AOS.init({
            duration: 800,
            easing: 'ease-in-out',
            once: false,
            mirror: true,
            offset: 120
        });

        // カウントアップアニメーション
        function animateValue(element, start, end, duration) {
            let startTimestamp = null;
            const step = (timestamp) => {
                if (!startTimestamp) startTimestamp = timestamp;
                const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                const current = Math.floor(progress * (end - start) + start);
                element.textContent = current.toLocaleString();
                if (progress < 1) {
                    window.requestAnimationFrame(step);
                }
            };
            window.requestAnimationFrame(step);
        }

        // Intersection Observerでカウントアップを制御
        const countElements = document.querySelectorAll('[data-aos="count-up"]');
        const countObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const numberElement = entry.target.querySelector('.stat-number');
                    const target = parseInt(numberElement.getAttribute('data-target'));
                    animateValue(numberElement, 0, target, 2000);
                    countObserver.unobserve(entry.target);
                }
            });
        }, { threshold: 0.5 });

        countElements.forEach(el => countObserver.observe(el));

        // スムーズスクロール
        document.addEventListener('click', (e) => {
            if (e.target.textContent === 'スクロールして体験') {
                window.scrollTo({
                    top: window.innerHeight,
                    behavior: 'smooth'
                });
            }
        });

        // デバッグ情報（開発用）
        console.log('AOS Version:', AOS.version || '2.3.1');
        console.log('AOS Settings:', {
            duration: 800,
            easing: 'ease-in-out',
            once: false,
            mirror: true,
            offset: 120
        });
    </script>
</body>
</html>
```

[^16]: AOS: https://michalsnik.github.io/aos/ - スクロールアニメーション専用ライブラリ
[^17]: Intersection Observer API: ブラウザのビューポートと要素の交差を効率的に監視するAPI

### 4.5 Chart.js 4系 - 美しいチャート作成ライブラリ

Chart.js[^18]は、Canvas要素を使用してレスポンシブで美しいチャートを作成するJavaScriptライブラリです。バージョン4.0では、Tree-shaking対応やESModules対応など、モダンな開発環境での利用が向上しています。

**特徴**:
- 8種類の基本チャート（線、棒、円、ドーナツ、レーダー、散布図、バブル、極面積図）
- レスポンシブデザイン対応
- インタラクティブ要素（ホバー、クリック、ツールチップ）
- 高度なカスタマイゼーション
- アニメーション効果内蔵

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.js`
- **cdnjs**: `https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js`
- **信頼性スコア**: 9/10
- **ファイルサイズ**: 約 190KB（minified）

**実用デモコード**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chart.js 4.4.1 実用デモ</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.js" 
            integrity="sha384-D3aQY8a+pBMhGd8TvtLHJSjr5z7aMCrZhvMIbJ6QLLhv6lS0L7w7s0+xKuqWpZfb" 
            crossorigin="anonymous"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
            background-color: #f5f7fa;
        }
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 30px;
            margin: 30px 0;
        }
        .chart-container {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 4px 16px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }
        .chart-container:hover {
            transform: translateY(-4px);
        }
        .chart-header {
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #e2e8f0;
        }
        .chart-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: #2d3748;
            margin: 0;
        }
        .chart-subtitle {
            font-size: 0.875rem;
            color: #718096;
            margin: 5px 0 0 0;
        }
        .controls {
            margin: 20px 0;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .btn {
            background: #4299e1;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.2s;
        }
        .btn:hover {
            background: #3182ce;
        }
        .btn-secondary {
            background: #718096;
        }
        .btn-secondary:hover {
            background: #4a5568;
        }
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }
        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            color: #4299e1;
        }
        .stat-label {
            font-size: 0.875rem;
            color: #718096;
            margin-top: 5px;
        }
        .data-table {
            margin: 20px 0;
            overflow-x: auto;
        }
        .data-table table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 8px;
            overflow: hidden;
        }
        .data-table th,
        .data-table td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #e2e8f0;
        }
        .data-table th {
            background: #f7fafc;
            font-weight: 600;
            color: #2d3748;
        }
        .trend-up { color: #48bb78; }
        .trend-down { color: #f56565; }
    </style>
</head>
<body>
    <h1>Chart.js 4.4.1 実用デモ</h1>
    <p>インタラクティブなチャートとダッシュボードの実装例</p>

    <!-- 統計サマリー -->
    <div class="stats">
        <div class="stat-card">
            <div class="stat-value" id="total-revenue">¥0</div>
            <div class="stat-label">総売上</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="total-orders">0</div>
            <div class="stat-label">注文数</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="avg-order">¥0</div>
            <div class="stat-label">平均注文額</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="growth-rate">0%</div>
            <div class="stat-label">成長率</div>
        </div>
    </div>

    <!-- チャートコントロール -->
    <div class="controls">
        <button class="btn" onclick="updateChartData()">データ更新</button>
        <button class="btn btn-secondary" onclick="toggleAnimation()">アニメーション切替</button>
        <button class="btn btn-secondary" onclick="exportChart()">PNG出力</button>
        <button class="btn btn-secondary" onclick="resetZoom()">ズームリセット</button>
    </div>

    <!-- チャートダッシュボード -->
    <div class="dashboard">
        <!-- 売上推移（線グラフ） -->
        <div class="chart-container">
            <div class="chart-header">
                <h3 class="chart-title">月別売上推移</h3>
                <p class="chart-subtitle">過去12ヶ月の売上トレンド</p>
            </div>
            <canvas id="revenueChart" width="400" height="200"></canvas>
        </div>

        <!-- 商品カテゴリ別売上（円グラフ） -->
        <div class="chart-container">
            <div class="chart-header">
                <h3 class="chart-title">カテゴリ別売上構成比</h3>
                <p class="chart-subtitle">商品カテゴリごとの売上割合</p>
            </div>
            <canvas id="categoryChart" width="400" height="200"></canvas>
        </div>

        <!-- 地域別売上（棒グラフ） -->
        <div class="chart-container">
            <div class="chart-header">
                <h3 class="chart-title">地域別売上比較</h3>
                <p class="chart-subtitle">各地域の売上実績</p>
            </div>
            <canvas id="regionChart" width="400" height="200"></canvas>
        </div>

        <!-- ユーザーエンゲージメント（レーダーチャート） -->
        <div class="chart-container">
            <div class="chart-header">
                <h3 class="chart-title">ユーザーエンゲージメント分析</h3>
                <p class="chart-subtitle">各指標のパフォーマンス</p>
            </div>
            <canvas id="engagementChart" width="400" height="200"></canvas>
        </div>
    </div>

    <!-- データテーブル -->
    <div class="data-table">
        <table>
            <thead>
                <tr>
                    <th>月</th>
                    <th>売上</th>
                    <th>注文数</th>
                    <th>成長率</th>
                    <th>トレンド</th>
                </tr>
            </thead>
            <tbody id="dataTableBody">
                <!-- 動的に生成 -->
            </tbody>
        </table>
    </div>

    <script>
        // チャートのグローバル設定
        Chart.defaults.font.family = '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif';
        Chart.defaults.color = '#4a5568';
        Chart.defaults.plugins.legend.position = 'bottom';

        let charts = {};
        let animationEnabled = true;

        // サンプルデータ
        const monthlyData = {
            labels: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
            datasets: [{
                label: '売上（万円）',
                data: [120, 135, 158, 172, 195, 218, 234, 256, 289, 312, 345, 378],
                borderColor: '#4299e1',
                backgroundColor: 'rgba(66, 153, 225, 0.1)',
                fill: true,
                tension: 0.4,
                pointRadius: 6,
                pointHoverRadius: 8
            }]
        };

        const categoryData = {
            labels: ['Electronics', 'Fashion', 'Books', 'Home & Garden', 'Sports'],
            datasets: [{
                data: [35, 25, 15, 15, 10],
                backgroundColor: [
                    '#4299e1',
                    '#48bb78',
                    '#ed8936',
                    '#9f7aea',
                    '#f56565'
                ],
                borderWidth: 0,
                hoverOffset: 10
            }]
        };

        const regionData = {
            labels: ['東京', '大阪', '名古屋', '福岡', '札幌', '仙台'],
            datasets: [{
                label: '売上（万円）',
                data: [450, 320, 280, 190, 150, 120],
                backgroundColor: [
                    '#4299e1',
                    '#48bb78',
                    '#ed8936',
                    '#9f7aea',
                    '#f56565',
                    '#38b2ac'
                ],
                borderRadius: 8,
                borderSkipped: false,
            }]
        };

        const engagementData = {
            labels: ['ページビュー', 'セッション時間', 'コンバージョン率', '顧客満足度', 'リピート率', 'SNSエンゲージメント'],
            datasets: [{
                label: '今月',
                data: [85, 78, 92, 88, 75, 82],
                borderColor: '#4299e1',
                backgroundColor: 'rgba(66, 153, 225, 0.3)',
                pointRadius: 6
            }, {
                label: '先月',
                data: [78, 72, 85, 83, 70, 76],
                borderColor: '#48bb78',
                backgroundColor: 'rgba(72, 187, 120, 0.3)',
                pointRadius: 6
            }]
        };

        // チャート初期化
        function initCharts() {
            // 売上推移チャート
            charts.revenue = new Chart(document.getElementById('revenueChart'), {
                type: 'line',
                data: monthlyData,
                options: {
                    responsive: true,
                    plugins: {
                        tooltip: {
                            backgroundColor: 'rgba(0,0,0,0.8)',
                            titleColor: '#fff',
                            bodyColor: '#fff',
                            borderColor: '#4299e1',
                            borderWidth: 1,
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': ¥' + context.parsed.y + '万円';
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return '¥' + value + '万';
                                }
                            }
                        }
                    },
                    interaction: {
                        intersect: false,
                        mode: 'index'
                    }
                }
            });

            // カテゴリ別売上チャート
            charts.category = new Chart(document.getElementById('categoryChart'), {
                type: 'doughnut',
                data: categoryData,
                options: {
                    responsive: true,
                    plugins: {
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.label + ': ' + context.parsed + '%';
                                }
                            }
                        }
                    }
                }
            });

            // 地域別売上チャート
            charts.region = new Chart(document.getElementById('regionChart'), {
                type: 'bar',
                data: regionData,
                options: {
                    responsive: true,
                    plugins: {
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': ¥' + context.parsed.y + '万円';
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return '¥' + value + '万';
                                }
                            }
                        }
                    }
                }
            });

            // エンゲージメントチャート
            charts.engagement = new Chart(document.getElementById('engagementChart'), {
                type: 'radar',
                data: engagementData,
                options: {
                    responsive: true,
                    scales: {
                        r: {
                            angleLines: {
                                display: true
                            },
                            suggestedMin: 0,
                            suggestedMax: 100
                        }
                    }
                }
            });
        }

        // 統計データ更新
        function updateStats() {
            const revenue = monthlyData.datasets[0].data.reduce((sum, val) => sum + val, 0);
            const orders = Math.floor(revenue * 2.3);
            const avgOrder = Math.floor(revenue * 10000 / orders);
            const growthRate = 12.5;

            document.getElementById('total-revenue').textContent = '¥' + revenue.toLocaleString() + '万';
            document.getElementById('total-orders').textContent = orders.toLocaleString();
            document.getElementById('avg-order').textContent = '¥' + avgOrder.toLocaleString();
            document.getElementById('growth-rate').textContent = '+' + growthRate + '%';
        }

        // データテーブル更新
        function updateDataTable() {
            const tbody = document.getElementById('dataTableBody');
            tbody.innerHTML = '';

            monthlyData.labels.forEach((month, index) => {
                const revenue = monthlyData.datasets[0].data[index];
                const orders = Math.floor(revenue * 2.3);
                const prevRevenue = index > 0 ? monthlyData.datasets[0].data[index - 1] : revenue;
                const growth = ((revenue - prevRevenue) / prevRevenue * 100).toFixed(1);
                const trend = growth > 0 ? '↗️' : growth < 0 ? '↘️' : '➡️';
                const trendClass = growth > 0 ? 'trend-up' : growth < 0 ? 'trend-down' : '';

                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${month}</td>
                    <td>¥${revenue}万</td>
                    <td>${orders.toLocaleString()}</td>
                    <td class="${trendClass}">${growth}%</td>
                    <td>${trend}</td>
                `;
            });
        }

        // データ更新機能
        function updateChartData() {
            // ランダムな変動を追加
            monthlyData.datasets[0].data = monthlyData.datasets[0].data.map(value => 
                Math.max(50, value + Math.floor((Math.random() - 0.5) * 40))
            );

            charts.revenue.update();
            updateStats();
            updateDataTable();
        }

        // アニメーション切替
        function toggleAnimation() {
            animationEnabled = !animationEnabled;
            Object.values(charts).forEach(chart => {
                chart.options.animation = animationEnabled;
                chart.update();
            });
        }

        // チャート出力
        function exportChart() {
            const canvas = document.getElementById('revenueChart');
            const url = canvas.toDataURL('image/png');
            const link = document.createElement('a');
            link.download = 'revenue-chart.png';
            link.href = url;
            link.click();
        }

        // ズームリセット
        function resetZoom() {
            Object.values(charts).forEach(chart => {
                if (chart.resetZoom) {
                    chart.resetZoom();
                }
            });
        }

        // 初期化
        document.addEventListener('DOMContentLoaded', function() {
            initCharts();
            updateStats();
            updateDataTable();
            
            console.log('Chart.js Version:', Chart.version);
            console.log('Charts initialized:', Object.keys(charts));
        });
    </script>
</body>
</html>
```

Chart.js の実用例では、4種類のチャート（線、円、棒、レーダー）を組み合わせたダッシュボードを作成しています。インタラクティブな要素やデータ更新機能も含めており、実際の業務システムでも応用できる構成となっています。

### 4.6 Swiper.js 11系 - モバイル対応スライダー

Swiper.js[^19]は、モバイルファーストで設計されたタッチスライダーライブラリです。iOS、Android、Desktop での快適なスワイプ操作を提供し、ネイティブアプリのような UX を Web で実現できます。

**特徴**:
- ネイティブライクなタッチ操作
- 50以上の設定オプション
- Virtual Slides機能（大量データ対応）
- パララックス効果・3D効果
- TypeScript完全対応

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/swiper@11.1.1/swiper-bundle.min.js`
- **Swiper CSS**: `https://cdn.jsdelivr.net/npm/swiper@11.1.1/swiper-bundle.min.css`
- **信頼性スコア**: 9/10
- **ファイルサイズ**: 約 140KB（JS + CSS、minified）

**実用デモコード**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Swiper.js 11.1.1 実用デモ</title>
    <link rel="stylesheet" 
          href="https://cdn.jsdelivr.net/npm/swiper@11.1.1/swiper-bundle.min.css"
          integrity="sha384-4OgHKvjmE43f5P8Uq0rOj2I45QdCMFE8FbKZf13HW2yN9HgSJ2ZPzRN2QfnYr4XZ"
          crossorigin="anonymous">
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .demo-section {
            margin: 60px 0;
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.15);
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .section-subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 40px;
            font-size: 1.1rem;
        }

        /* ヒーロースライダー */
        .hero-swiper {
            height: 500px;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .hero-slide {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            font-weight: bold;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            position: relative;
            overflow: hidden;
        }

        .hero-slide::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.3);
            z-index: 1;
        }

        .hero-content {
            z-index: 2;
            text-align: center;
            padding: 20px;
        }

        .hero-title {
            font-size: 3rem;
            margin-bottom: 20px;
            animation: slideInUp 1s ease-out;
        }

        .hero-text {
            font-size: 1.2rem;
            margin-bottom: 30px;
            animation: slideInUp 1s ease-out 0.2s both;
        }

        .hero-btn {
            background: rgba(255,255,255,0.2);
            border: 2px solid white;
            color: white;
            padding: 15px 30px;
            border-radius: 50px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: slideInUp 1s ease-out 0.4s both;
        }

        .hero-btn:hover {
            background: white;
            color: #333;
            transform: translateY(-2px);
        }

        /* 商品スライダー */
        .products-swiper {
            padding: 20px 0 60px 0;
        }

        .product-card {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            text-align: center;
            height: 280px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .product-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.15);
        }

        .product-icon {
            font-size: 4rem;
            margin-bottom: 20px;
        }

        .product-title {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 10px;
            color: #2d3748;
        }

        .product-price {
            font-size: 1.5rem;
            font-weight: bold;
            color: #667eea;
            margin-bottom: 15px;
        }

        .product-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 25px;
            cursor: pointer;
            transition: transform 0.2s ease;
        }

        .product-btn:hover {
            transform: scale(1.05);
        }

        /* 垂直スライダー */
        .vertical-swiper {
            height: 400px;
            width: 300px;
            margin: 0 auto;
        }

        .vertical-slide {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: white;
            border-radius: 10px;
            margin: 10px 0;
        }

        /* サムネイル付きギャラリー */
        .gallery-main {
            height: 400px;
            margin-bottom: 10px;
        }

        .gallery-thumbs {
            height: 80px;
            padding: 0 20px;
        }

        .gallery-thumbs .swiper-slide {
            opacity: 0.4;
            cursor: pointer;
        }

        .gallery-thumbs .swiper-slide-thumb-active {
            opacity: 1;
        }

        .gallery-slide {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: white;
            border-radius: 10px;
            background: linear-gradient(45deg, #667eea, #764ba2);
        }

        /* レスポンシブ対応 */
        @media (max-width: 768px) {
            .hero-title { font-size: 2rem; }
            .hero-text { font-size: 1rem; }
            .vertical-swiper { width: 280px; height: 350px; }
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Swiper カスタマイズ */
        .swiper-pagination-bullet-active {
            background: #667eea !important;
        }

        .swiper-button-next,
        .swiper-button-prev {
            color: #667eea !important;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .stat-item {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 30px 20px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .stat-label {
            font-size: 1rem;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <!-- ヒーローセクション -->
    <div class="demo-section">
        <h2 class="section-title">Hero Slider</h2>
        <p class="section-subtitle">フルスクリーンヒーロースライダーの実装例</p>
        
        <div class="swiper hero-swiper">
            <div class="swiper-wrapper">
                <div class="swiper-slide hero-slide" 
                     style="background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), 
                            url('data:image/svg+xml,<svg xmlns=&quot;http://www.w3.org/2000/svg&quot; viewBox=&quot;0 0 1000 600&quot;><rect fill=&quot;%23ff6b6b&quot; width=&quot;1000&quot; height=&quot;600&quot;/><circle fill=&quot;%23ffa726&quot; cx=&quot;200&quot; cy=&quot;150&quot; r=&quot;100&quot;/><circle fill=&quot;%2366bb6a&quot; cx=&quot;800&quot; cy=&quot;450&quot; r=&quot;120&quot;/></svg>'); 
                            background-size: cover;">
                    <div class="hero-content">
                        <h1 class="hero-title">革新的なサービス</h1>
                        <p class="hero-text">未来を創造する最先端テクノロジー</p>
                        <button class="hero-btn">今すぐ始める</button>
                    </div>
                </div>
                <div class="swiper-slide hero-slide" 
                     style="background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), 
                            url('data:image/svg+xml,<svg xmlns=&quot;http://www.w3.org/2000/svg&quot; viewBox=&quot;0 0 1000 600&quot;><rect fill=&quot;%234ecdc4&quot; width=&quot;1000&quot; height=&quot;600&quot;/><polygon fill=&quot;%239b59b6&quot; points=&quot;100,100 400,150 300,400&quot;/><polygon fill=&quot;%23f39c12&quot; points=&quot;600,200 900,100 850,500&quot;/></svg>'); 
                            background-size: cover;">
                    <div class="hero-content">
                        <h1 class="hero-title">グローバル展開</h1>
                        <p class="hero-text">世界中のお客様にサービスを提供</p>
                        <button class="hero-btn">詳しく見る</button>
                    </div>
                </div>
                <div class="swiper-slide hero-slide" 
                     style="background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), 
                            url('data:image/svg+xml,<svg xmlns=&quot;http://www.w3.org/2000/svg&quot; viewBox=&quot;0 0 1000 600&quot;><rect fill=&quot;%23667eea&quot; width=&quot;1000&quot; height=&quot;600&quot;/><rect fill=&quot;%23764ba2&quot; x=&quot;200&quot; y=&quot;200&quot; width=&quot;600&quot; height=&quot;200&quot; opacity=&quot;0.8&quot;/></svg>'); 
                            background-size: cover;">
                    <div class="hero-content">
                        <h1 class="hero-title">安心・安全</h1>
                        <p class="hero-text">最高レベルのセキュリティを保証</p>
                        <button class="hero-btn">お問い合わせ</button>
                    </div>
                </div>
            </div>
            <div class="swiper-pagination"></div>
            <div class="swiper-button-next"></div>
            <div class="swiper-button-prev"></div>
        </div>
    </div>

    <!-- 商品スライダー -->
    <div class="demo-section">
        <h2 class="section-title">Product Showcase</h2>
        <p class="section-subtitle">レスポンシブ商品カルーセル</p>
        
        <div class="swiper products-swiper">
            <div class="swiper-wrapper">
                <div class="swiper-slide">
                    <div class="product-card">
                        <div class="product-icon">💻</div>
                        <div class="product-title">プレミアムラップトップ</div>
                        <div class="product-price">¥299,800</div>
                        <button class="product-btn">カートに追加</button>
                    </div>
                </div>
                <div class="swiper-slide">
                    <div class="product-card">
                        <div class="product-icon">📱</div>
                        <div class="product-title">最新スマートフォン</div>
                        <div class="product-price">¥128,800</div>
                        <button class="product-btn">カートに追加</button>
                    </div>
                </div>
                <div class="swiper-slide">
                    <div class="product-card">
                        <div class="product-icon">🎧</div>
                        <div class="product-title">ノイズキャンセリング<br>ヘッドフォン</div>
                        <div class="product-price">¥45,800</div>
                        <button class="product-btn">カートに追加</button>
                    </div>
                </div>
                <div class="swiper-slide">
                    <div class="product-card">
                        <div class="product-icon">⌚</div>
                        <div class="product-title">スマートウォッチ</div>
                        <div class="product-price">¥68,800</div>
                        <button class="product-btn">カートに追加</button>
                    </div>
                </div>
                <div class="swiper-slide">
                    <div class="product-card">
                        <div class="product-icon">📷</div>
                        <div class="product-title">ミラーレスカメラ</div>
                        <div class="product-price">¥185,800</div>
                        <button class="product-btn">カートに追加</button>
                    </div>
                </div>
                <div class="swiper-slide">
                    <div class="product-card">
                        <div class="product-icon">🖥️</div>
                        <div class="product-title">4Kモニター</div>
                        <div class="product-price">¥89,800</div>
                        <button class="product-btn">カートに追加</button>
                    </div>
                </div>
            </div>
            <div class="swiper-pagination"></div>
        </div>
    </div>

    <!-- 統計情報 -->
    <div class="demo-section">
        <h2 class="section-title">Performance Stats</h2>
        <div class="stats-grid">
            <div class="stat-item">
                <div class="stat-number" id="users-count">0</div>
                <div class="stat-label">アクティブユーザー</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="downloads-count">0</div>
                <div class="stat-label">総ダウンロード数</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="projects-count">0</div>
                <div class="stat-label">プロジェクト数</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="satisfaction-count">0</div>
                <div class="stat-label">満足度 %</div>
            </div>
        </div>
    </div>

    <!-- 垂直スライダー -->
    <div class="demo-section">
        <h2 class="section-title">Vertical Slider</h2>
        <p class="section-subtitle">縦方向スクロールスライダー</p>
        
        <div class="swiper vertical-swiper">
            <div class="swiper-wrapper">
                <div class="swiper-slide vertical-slide" style="background: linear-gradient(45deg, #ff6b6b, #ee5a52);">
                    <div>🚀 Innovation</div>
                </div>
                <div class="swiper-slide vertical-slide" style="background: linear-gradient(45deg, #4ecdc4, #44a08d);">
                    <div>💡 Creativity</div>
                </div>
                <div class="swiper-slide vertical-slide" style="background: linear-gradient(45deg, #45b7d1, #96c93d);">
                    <div>⚡ Performance</div>
                </div>
                <div class="swiper-slide vertical-slide" style="background: linear-gradient(45deg, #f093fb, #f5576c);">
                    <div>🎯 Precision</div>
                </div>
                <div class="swiper-slide vertical-slide" style="background: linear-gradient(45deg, #4facfe, #00f2fe);">
                    <div>🌟 Excellence</div>
                </div>
            </div>
            <div class="swiper-pagination"></div>
        </div>
    </div>

    <!-- ギャラリー（サムネイル付き） -->
    <div class="demo-section">
        <h2 class="section-title">Thumbnail Gallery</h2>
        <p class="section-subtitle">サムネイル連動ギャラリー</p>
        
        <div class="swiper gallery-main">
            <div class="swiper-wrapper">
                <div class="swiper-slide gallery-slide">🎨 Artwork 1</div>
                <div class="swiper-slide gallery-slide">🖼️ Artwork 2</div>
                <div class="swiper-slide gallery-slide">🎭 Artwork 3</div>
                <div class="swiper-slide gallery-slide">🏛️ Artwork 4</div>
                <div class="swiper-slide gallery-slide">🎪 Artwork 5</div>
            </div>
        </div>
        
        <div class="swiper gallery-thumbs">
            <div class="swiper-wrapper">
                <div class="swiper-slide gallery-slide">🎨</div>
                <div class="swiper-slide gallery-slide">🖼️</div>
                <div class="swiper-slide gallery-slide">🎭</div>
                <div class="swiper-slide gallery-slide">🏛️</div>
                <div class="swiper-slide gallery-slide">🎪</div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/swiper@11.1.1/swiper-bundle.min.js"
            integrity="sha384-A3K3r0d6lJfHZJj+rYIxP1e6ZdA7YlC2/qgJ5o9W3WN8vCXUJ5kYpzIy7bYjYd1a"
            crossorigin="anonymous"></script>
    <script>
        // ヒーロースライダー
        const heroSwiper = new Swiper('.hero-swiper', {
            loop: true,
            autoplay: {
                delay: 5000,
                disableOnInteraction: false,
            },
            pagination: {
                el: '.hero-swiper .swiper-pagination',
                clickable: true,
            },
            navigation: {
                nextEl: '.hero-swiper .swiper-button-next',
                prevEl: '.hero-swiper .swiper-button-prev',
            },
            effect: 'fade',
            fadeEffect: {
                crossFade: true
            },
            speed: 1000,
        });

        // 商品スライダー
        const productsSwiper = new Swiper('.products-swiper', {
            slidesPerView: 1,
            spaceBetween: 20,
            loop: true,
            autoplay: {
                delay: 3000,
                disableOnInteraction: false,
            },
            pagination: {
                el: '.products-swiper .swiper-pagination',
                clickable: true,
                dynamicBullets: true,
            },
            breakpoints: {
                576: {
                    slidesPerView: 2,
                },
                768: {
                    slidesPerView: 3,
                },
                1024: {
                    slidesPerView: 4,
                }
            },
            centeredSlides: false,
        });

        // 垂直スライダー
        const verticalSwiper = new Swiper('.vertical-swiper', {
            direction: 'vertical',
            slidesPerView: 3,
            spaceBetween: 20,
            centeredSlides: true,
            loop: true,
            autoplay: {
                delay: 2500,
                disableOnInteraction: false,
            },
            pagination: {
                el: '.vertical-swiper .swiper-pagination',
                clickable: true,
            },
            mousewheel: true,
        });

        // サムネイル付きギャラリー
        const galleryThumbs = new Swiper('.gallery-thumbs', {
            spaceBetween: 10,
            slidesPerView: 5,
            freeMode: true,
            watchSlidesProgress: true,
        });

        const galleryMain = new Swiper('.gallery-main', {
            spaceBetween: 10,
            thumbs: {
                swiper: galleryThumbs,
            },
            loop: true,
            autoplay: {
                delay: 4000,
                disableOnInteraction: false,
            },
        });

        // カウンターアニメーション
        function animateCounter(element, target, duration = 2000) {
            let start = 0;
            const increment = target / (duration / 16);
            const timer = setInterval(() => {
                start += increment;
                element.textContent = Math.floor(start).toLocaleString();
                if (start >= target) {
                    element.textContent = target.toLocaleString();
                    clearInterval(timer);
                }
            }, 16);
        }

        // ページ読み込み時のアニメーション
        window.addEventListener('load', () => {
            setTimeout(() => {
                animateCounter(document.getElementById('users-count'), 125000);
                animateCounter(document.getElementById('downloads-count'), 2500000);
                animateCounter(document.getElementById('projects-count'), 15000);
                animateCounter(document.getElementById('satisfaction-count'), 98);
            }, 500);
        });

        // ボタンクリックイベント
        document.querySelectorAll('.product-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                this.textContent = '追加済み ✓';
                this.style.background = '#48bb78';
                setTimeout(() => {
                    this.textContent = 'カートに追加';
                    this.style.background = 'linear-gradient(45deg, #667eea, #764ba2)';
                }, 2000);
            });
        });

        document.querySelectorAll('.hero-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                alert('ボタンがクリックされました: ' + this.textContent);
            });
        });

        // デバッグ情報
        console.log('Swiper Version:', Swiper.version || '11.1.1');
        console.log('Initialized Swipers:', {
            hero: heroSwiper,
            products: productsSwiper,
            vertical: verticalSwiper,
            gallery: { main: galleryMain, thumbs: galleryThumbs }
        });

        // レスポンシブブレークポイント監視
        window.addEventListener('resize', () => {
            console.log('Window size:', window.innerWidth + 'x' + window.innerHeight);
        });
    </script>
</body>
</html>
```

Swiper.js の実装では、ヒーロースライダー、商品カルーセル、垂直スライダー、サムネイル付きギャラリーなど、実際のWebサイトで使用される典型的なパターンを網羅しています。モバイル対応やタッチ操作も完全にサポートされています。

[^18]: Chart.js: https://www.chartjs.org/ - Canvas ベースチャートライブラリ
[^19]: Swiper.js: https://swiperjs.com/ - モバイルタッチスライダー

### 4.7 Day.js 1系 - 軽量日時ライブラリ

Day.js[^20]は、Moment.js の軽量代替として設計されたモダンな日時処理ライブラリです。同じAPIを維持しながら、わずか 2KB のサイズで最新のJavaScript環境に最適化されています。

**特徴**:
- Moment.js 互換API
- 軽量設計（2KB minified + gzipped）
- Immutable（変更不可能）なデータ操作
- プラグインシステム対応
- TypeScript完全対応

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/dayjs@1.11.10/dayjs.min.js`
- **cdnjs**: `https://cdnjs.cloudflare.com/ajax/libs/dayjs/1.11.10/dayjs.min.js`
- **信頼性スコア**: 9/10
- **ファイルサイズ**: 約 2KB（minified + gzipped）

**実用デモコード**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Day.js 1.11.10 実用デモ</title>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/dayjs.min.js"
            integrity="sha384-fww6xHa6+AKBwEK5ZOxfyCAONrU/w6xIm1nGUw6TlZKrMWKgvmOmBsP3mNY5W1yf"
            crossorigin="anonymous"></script>
    <!-- プラグイン -->
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/plugin/relativeTime.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/plugin/customParseFormat.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/plugin/duration.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/plugin/calendar.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/plugin/timezone.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/plugin/utc.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/locale/ja.js"></script>
    
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #74b9ff 0%, #0984e3 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .main-title {
            text-align: center;
            color: white;
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .subtitle {
            text-align: center;
            color: rgba(255,255,255,0.9);
            font-size: 1.1rem;
            margin-bottom: 40px;
        }
        
        .demo-section {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin: 25px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }
        
        .section-title {
            font-size: 1.8rem;
            color: #2d3436;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #74b9ff;
        }
        
        .demo-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }
        
        .demo-item {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #74b9ff;
        }
        
        .demo-label {
            font-weight: bold;
            color: #2d3436;
            margin-bottom: 8px;
            font-size: 1rem;
        }
        
        .demo-value {
            font-family: 'Courier New', monospace;
            background: #2d3436;
            color: #00b894;
            padding: 12px;
            border-radius: 6px;
            font-size: 0.9rem;
            word-break: break-all;
        }
        
        .controls {
            display: flex;
            gap: 10px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        .btn {
            background: #74b9ff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.2s;
        }
        
        .btn:hover {
            background: #0984e3;
        }
        
        .btn-secondary {
            background: #636e72;
        }
        
        .btn-secondary:hover {
            background: #2d3436;
        }
        
        .input-group {
            margin: 15px 0;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #2d3436;
        }
        
        .input-group input, 
        .input-group select {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
            box-sizing: border-box;
        }
        
        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: #74b9ff;
        }
        
        .clock {
            text-align: center;
            font-size: 3rem;
            font-weight: bold;
            color: #74b9ff;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            margin: 20px 0;
            font-family: 'Courier New', monospace;
        }
        
        .timezone-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .timezone-item {
            background: linear-gradient(45deg, #74b9ff, #0984e3);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }
        
        .timezone-city {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 8px;
        }
        
        .timezone-time {
            font-family: 'Courier New', monospace;
            font-size: 1.3rem;
        }
        
        .calendar-view {
            background: #f1f2f6;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }
        
        .event-list {
            max-height: 300px;
            overflow-y: auto;
            margin: 20px 0;
        }
        
        .event-item {
            background: white;
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            border-left: 4px solid #74b9ff;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        
        .event-time {
            font-weight: bold;
            color: #74b9ff;
            font-size: 0.9rem;
        }
        
        .event-title {
            font-size: 1.1rem;
            margin: 5px 0;
            color: #2d3436;
        }
        
        .event-relative {
            font-size: 0.85rem;
            color: #636e72;
        }
        
        .stats-section {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin: 25px 0;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            color: white;
            padding: 25px;
            border-radius: 12px;
            text-align: center;
        }
        
        .stat-number {
            font-size: 2.2rem;
            font-weight: bold;
            margin-bottom: 8px;
            font-family: 'Courier New', monospace;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <h1 class="main-title">Day.js 実用デモ</h1>
    <p class="subtitle">軽量でパワフルな日時処理ライブラリの完全活用例</p>

    <!-- 現在時刻表示 -->
    <div class="demo-section">
        <h2 class="section-title">リアルタイムクロック</h2>
        <div class="clock" id="current-time">--:--:--</div>
        <div class="demo-grid">
            <div class="demo-item">
                <div class="demo-label">Unix タイムスタンプ</div>
                <div class="demo-value" id="timestamp">0</div>
            </div>
            <div class="demo-item">
                <div class="demo-label">ISO 8601 フォーマット</div>
                <div class="demo-value" id="iso-format">--</div>
            </div>
            <div class="demo-item">
                <div class="demo-label">日本語表記</div>
                <div class="demo-value" id="japanese-format">--</div>
            </div>
            <div class="demo-item">
                <div class="demo-label">相対時間</div>
                <div class="demo-value" id="relative-time">--</div>
            </div>
        </div>
    </div>

    <!-- 世界時計 -->
    <div class="demo-section">
        <h2 class="section-title">世界時計</h2>
        <div class="timezone-grid" id="world-clocks">
            <!-- 動的に生成 -->
        </div>
    </div>

    <!-- フォーマット機能 -->
    <div class="demo-section">
        <h2 class="section-title">日付フォーマット変換</h2>
        <div class="input-group">
            <label for="date-input">日付を入力してください</label>
            <input type="datetime-local" id="date-input">
        </div>
        <div class="controls">
            <button class="btn" onclick="formatExamples()">フォーマット例を表示</button>
            <button class="btn btn-secondary" onclick="clearFormats()">クリア</button>
        </div>
        <div class="demo-grid" id="format-results">
            <!-- 動的に生成 -->
        </div>
    </div>

    <!-- 日付計算機能 -->
    <div class="demo-section">
        <h2 class="section-title">日付計算機</h2>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
            <div>
                <div class="input-group">
                    <label for="calc-date1">開始日</label>
                    <input type="date" id="calc-date1">
                </div>
                <div class="input-group">
                    <label for="calc-date2">終了日</label>
                    <input type="date" id="calc-date2">
                </div>
                <button class="btn" onclick="calculateDifference()">差分を計算</button>
            </div>
            <div class="demo-grid" id="calc-results">
                <!-- 計算結果表示 -->
            </div>
        </div>
    </div>

    <!-- イベントスケジューラー -->
    <div class="demo-section">
        <h2 class="section-title">イベントスケジューラー</h2>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 30px;">
            <div>
                <div class="input-group">
                    <label for="event-title">イベント名</label>
                    <input type="text" id="event-title" placeholder="会議、誕生日、旅行など">
                </div>
                <div class="input-group">
                    <label for="event-datetime">日時</label>
                    <input type="datetime-local" id="event-datetime">
                </div>
                <button class="btn" onclick="addEvent()">イベント追加</button>
                <button class="btn btn-secondary" onclick="clearEvents()">全てクリア</button>
            </div>
            <div>
                <h3>登録済みイベント</h3>
                <div class="event-list" id="event-list">
                    <!-- イベント一覧表示 -->
                </div>
            </div>
        </div>
    </div>

    <!-- 統計情報 -->
    <div class="demo-section">
        <h2 class="section-title">時間統計</h2>
        <div class="stats-section">
            <div class="stat-card">
                <div class="stat-number" id="days-this-year">0</div>
                <div class="stat-label">今年経過日数</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="days-remaining">0</div>
                <div class="stat-label">今年残り日数</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="weeks-this-month">0</div>
                <div class="stat-label">今月の週数</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="age-in-days">0</div>
                <div class="stat-label">生後日数 (例)</div>
            </div>
        </div>
    </div>

    <script>
        // Day.js プラグイン設定
        dayjs.extend(dayjs_plugin_relativeTime);
        dayjs.extend(dayjs_plugin_customParseFormat);
        dayjs.extend(dayjs_plugin_duration);
        dayjs.extend(dayjs_plugin_calendar);
        dayjs.extend(dayjs_plugin_timezone);
        dayjs.extend(dayjs_plugin_utc);
        dayjs.locale('ja');

        // イベントストレージ
        let events = [];

        // 世界時計のタイムゾーン設定
        const worldTimezones = [
            { city: '東京', timezone: 'Asia/Tokyo' },
            { city: 'ニューヨーク', timezone: 'America/New_York' },
            { city: 'ロンドン', timezone: 'Europe/London' },
            { city: 'パリ', timezone: 'Europe/Paris' },
            { city: 'シドニー', timezone: 'Australia/Sydney' },
            { city: 'ソウル', timezone: 'Asia/Seoul' }
        ];

        // リアルタイム更新
        function updateClock() {
            const now = dayjs();
            
            // 基本表示更新
            document.getElementById('current-time').textContent = now.format('HH:mm:ss');
            document.getElementById('timestamp').textContent = now.unix();
            document.getElementById('iso-format').textContent = now.toISOString();
            document.getElementById('japanese-format').textContent = now.format('YYYY年MM月DD日 dddd HH:mm:ss');
            document.getElementById('relative-time').textContent = '現在';
            
            // 世界時計更新
            updateWorldClocks();
            
            // 統計情報更新
            updateStats();
            
            // イベントリスト更新
            updateEventList();
        }

        // 世界時計更新
        function updateWorldClocks() {
            const container = document.getElementById('world-clocks');
            container.innerHTML = '';
            
            worldTimezones.forEach(zone => {
                const time = dayjs().tz(zone.timezone);
                const div = document.createElement('div');
                div.className = 'timezone-item';
                div.innerHTML = `
                    <div class="timezone-city">${zone.city}</div>
                    <div class="timezone-time">${time.format('HH:mm')}</div>
                    <div style="font-size: 0.8rem; opacity: 0.8;">${time.format('MM/DD')}</div>
                `;
                container.appendChild(div);
            });
        }

        // フォーマット例表示
        function formatExamples() {
            const input = document.getElementById('date-input').value;
            const container = document.getElementById('format-results');
            
            if (!input) {
                container.innerHTML = '<div class="demo-item"><div class="demo-value">日付を入力してください</div></div>';
                return;
            }
            
            const date = dayjs(input);
            const formats = [
                { label: '基本形式', value: date.format('YYYY-MM-DD HH:mm:ss') },
                { label: '日本語形式', value: date.format('YYYY年MM月DD日 dddd') },
                { label: 'アメリカ形式', value: date.format('MM/DD/YYYY hh:mm A') },
                { label: 'ISO形式', value: date.toISOString() },
                { label: '相対時間', value: date.fromNow() },
                { label: 'カレンダー', value: date.calendar() },
                { label: 'Unixタイム', value: date.unix().toString() },
                { label: '月の名前', value: date.format('MMMM YYYY') }
            ];
            
            container.innerHTML = formats.map(fmt => `
                <div class="demo-item">
                    <div class="demo-label">${fmt.label}</div>
                    <div class="demo-value">${fmt.value}</div>
                </div>
            `).join('');
        }

        // フォーマット結果クリア
        function clearFormats() {
            document.getElementById('format-results').innerHTML = '';
            document.getElementById('date-input').value = '';
        }

        // 日付差分計算
        function calculateDifference() {
            const date1 = dayjs(document.getElementById('calc-date1').value);
            const date2 = dayjs(document.getElementById('calc-date2').value);
            const container = document.getElementById('calc-results');
            
            if (!date1.isValid() || !date2.isValid()) {
                container.innerHTML = '<div class="demo-item"><div class="demo-value">有効な日付を入力してください</div></div>';
                return;
            }
            
            const diff = date2.diff(date1);
            const duration = dayjs.duration(diff);
            
            const results = [
                { label: '日数差', value: `${Math.abs(date2.diff(date1, 'day'))} 日` },
                { label: '時間差', value: `${Math.abs(date2.diff(date1, 'hour'))} 時間` },
                { label: '分差', value: `${Math.abs(date2.diff(date1, 'minute'))} 分` },
                { label: '詳細', value: `${Math.abs(duration.years())}年 ${Math.abs(duration.months())}ヶ月 ${Math.abs(duration.days())}日` }
            ];
            
            container.innerHTML = results.map(result => `
                <div class="demo-item">
                    <div class="demo-label">${result.label}</div>
                    <div class="demo-value">${result.value}</div>
                </div>
            `).join('');
        }

        // イベント追加
        function addEvent() {
            const title = document.getElementById('event-title').value.trim();
            const datetime = document.getElementById('event-datetime').value;
            
            if (!title || !datetime) {
                alert('イベント名と日時を入力してください');
                return;
            }
            
            events.push({
                id: Date.now(),
                title: title,
                datetime: dayjs(datetime)
            });
            
            // フィールドクリア
            document.getElementById('event-title').value = '';
            document.getElementById('event-datetime').value = '';
            
            updateEventList();
        }

        // イベント一覧更新
        function updateEventList() {
            const container = document.getElementById('event-list');
            
            if (events.length === 0) {
                container.innerHTML = '<div style="text-align: center; padding: 20px; color: #636e72;">イベントが登録されていません</div>';
                return;
            }
            
            // 日時順でソート
            const sortedEvents = events.sort((a, b) => a.datetime - b.datetime);
            
            container.innerHTML = sortedEvents.map(event => `
                <div class="event-item">
                    <div class="event-time">${event.datetime.format('YYYY年MM月DD日 HH:mm')}</div>
                    <div class="event-title">${event.title}</div>
                    <div class="event-relative">${event.datetime.fromNow()}</div>
                </div>
            `).join('');
        }

        // 全イベントクリア
        function clearEvents() {
            events = [];
            updateEventList();
        }

        // 統計情報更新
        function updateStats() {
            const now = dayjs();
            const startOfYear = dayjs().startOf('year');
            const endOfYear = dayjs().endOf('year');
            const birthDate = dayjs('1990-01-01'); // 例: 1990年生まれ
            
            document.getElementById('days-this-year').textContent = now.diff(startOfYear, 'day');
            document.getElementById('days-remaining').textContent = endOfYear.diff(now, 'day');
            document.getElementById('weeks-this-month').textContent = Math.ceil(now.date() / 7);
            document.getElementById('age-in-days').textContent = now.diff(birthDate, 'day').toLocaleString();
        }

        // 初期化とタイマー設定
        document.addEventListener('DOMContentLoaded', function() {
            // 現在時刻を入力フィールドにセット
            document.getElementById('date-input').value = dayjs().format('YYYY-MM-DDTHH:mm');
            document.getElementById('calc-date1').value = dayjs().format('YYYY-MM-DD');
            document.getElementById('calc-date2').value = dayjs().add(30, 'day').format('YYYY-MM-DD');
            document.getElementById('event-datetime').value = dayjs().add(1, 'hour').format('YYYY-MM-DDTHH:mm');
            
            // 初回更新
            updateClock();
            
            // 1秒ごとに更新
            setInterval(updateClock, 1000);
            
            // デバッグ情報
            console.log('Day.js Version:', dayjs.version || '1.11.10');
            console.log('Day.js Locale:', dayjs.locale());
            console.log('Available Plugins:', {
                relativeTime: !!dayjs.fn.fromNow,
                customParseFormat: !!dayjs.fn.customParseFormat,
                duration: !!dayjs.duration,
                calendar: !!dayjs.fn.calendar,
                timezone: !!dayjs.tz,
                utc: !!dayjs.utc
            });
        });
    </script>
</body>
</html>
```

Day.js の実装では、リアルタイムクロック、世界時計、日付フォーマット変換、日付計算、イベントスケジューラーなど、日時処理の実用的な機能を網羅しています。プラグインシステムを活用した高度な機能も含まれています。

### 4.8 Lodash 4系 - JavaScript ユーティリティライブラリ

Lodash[^21]は、JavaScript の関数型プログラミングを支援する包括的なユーティリティライブラリです。配列、オブジェクト、関数操作において、ネイティブ JavaScript では複雑になる処理を簡潔に書けます。

**特徴**:
- 300以上のユーティリティ関数
- 関数型プログラミング対応
- 不変性（Immutability）サポート
- パフォーマンス最適化
- モジュラー設計（個別インポート可能）

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js`
- **cdnjs**: `https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.21/lodash.min.js`
- **信頼性スコア**: 10/10
- **ファイルサイズ**: 約 70KB（minified + gzipped）

**実用デモコード**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lodash 4.17.21 実用デモ</title>
    <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"
            integrity="sha384-f/MGzD4CQCaF0p7FccxT5p6+p9XNPZk3W/tJJYPZhO9UO9ohrx+kZKdN+OiOF9/U"
            crossorigin="anonymous"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
        }
        
        .main-title {
            font-size: 2.8rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .demo-section {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin: 25px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }
        
        .section-title {
            font-size: 1.8rem;
            color: #2d3436;
            margin-bottom: 25px;
            padding-bottom: 10px;
            border-bottom: 3px solid #667eea;
        }
        
        .demo-group {
            margin: 30px 0;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
            border-left: 4px solid #667eea;
        }
        
        .demo-title {
            font-size: 1.3rem;
            color: #2d3436;
            margin-bottom: 15px;
            font-weight: 600;
        }
        
        .code-block {
            background: #2d3436;
            color: #00b894;
            padding: 15px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            margin: 10px 0;
            overflow-x: auto;
            white-space: pre-wrap;
        }
        
        .result-block {
            background: #e8f5e8;
            border: 1px solid #00b894;
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
        }
        
        .controls {
            display: flex;
            gap: 10px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        .btn {
            background: #667eea;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.2s;
        }
        
        .btn:hover {
            background: #5a67d8;
        }
        
        .btn-secondary {
            background: #636e72;
        }
        
        .btn-secondary:hover {
            background: #2d3436;
        }
        
        .input-section {
            margin: 20px 0;
        }
        
        .input-group {
            margin: 15px 0;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #2d3436;
        }
        
        .input-group input, 
        .input-group textarea {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
            box-sizing: border-box;
            font-family: 'Courier New', monospace;
        }
        
        .input-group input:focus,
        .input-group textarea:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .performance-section {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }
        
        .perf-item {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 12px;
            text-align: center;
        }
        
        .perf-title {
            font-size: 1.1rem;
            margin-bottom: 10px;
            font-weight: 600;
        }
        
        .perf-time {
            font-size: 2rem;
            font-weight: bold;
            font-family: 'Courier New', monospace;
        }
        
        .perf-unit {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .data-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .data-table th,
        .data-table td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        
        .data-table th {
            background: #667eea;
            color: white;
            font-weight: 600;
        }
        
        .data-table tbody tr:hover {
            background: #f8f9fa;
        }
        
        .highlight {
            background: #fff3cd;
            padding: 2px 4px;
            border-radius: 3px;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1 class="main-title">Lodash 実用デモ</h1>
        <p class="subtitle">JavaScript ユーティリティライブラリの完全活用例</p>
    </div>

    <!-- 配列操作 -->
    <div class="demo-section">
        <h2 class="section-title">配列操作（Array Methods）</h2>
        
        <div class="demo-group">
            <h3 class="demo-title">1. データ変換・フィルタリング</h3>
            <div class="code-block" id="array-code">// 実行ボタンを押してコードを確認</div>
            <div class="controls">
                <button class="btn" onclick="demonstrateArrayMethods()">配列操作デモ実行</button>
                <button class="btn btn-secondary" onclick="clearArrayResults()">結果クリア</button>
            </div>
            <div id="array-results"></div>
        </div>
    </div>

    <!-- オブジェクト操作 -->
    <div class="demo-section">
        <h2 class="section-title">オブジェクト操作（Object Methods）</h2>
        
        <div class="demo-group">
            <h3 class="demo-title">2. 深いコピーとマージ</h3>
            <div class="input-section">
                <div class="input-group">
                    <label for="object-input">JSON オブジェクト（編集してテスト）</label>
                    <textarea id="object-input" rows="8">{
  "user": {
    "name": "田中太郎",
    "age": 30,
    "address": {
      "city": "東京",
      "zip": "100-0001"
    }
  },
  "settings": {
    "theme": "dark",
    "notifications": true
  }
}</textarea>
                </div>
            </div>
            <div class="controls">
                <button class="btn" onclick="demonstrateObjectMethods()">オブジェクト操作デモ</button>
                <button class="btn btn-secondary" onclick="resetObjectInput()">入力リセット</button>
            </div>
            <div id="object-results"></div>
        </div>
    </div>

    <!-- 関数操作 -->
    <div class="demo-section">
        <h2 class="section-title">関数操作（Function Methods）</h2>
        
        <div class="demo-group">
            <h3 class="demo-title">3. デバウンス・スロットリング</h3>
            <div class="controls">
                <button class="btn" id="debounced-btn">デバウンス（500ms）</button>
                <button class="btn" id="throttled-btn">スロットリング（1000ms）</button>
                <button class="btn btn-secondary" onclick="resetFunctionCounts()">カウントリセット</button>
            </div>
            <div id="function-results">
                <div style="margin: 20px 0;">
                    <strong>実行回数:</strong> デバウンス <span id="debounce-count">0</span>回, スロットリング <span id="throttle-count">0</span>回
                </div>
            </div>
        </div>
    </div>

    <!-- データ処理パイプライン -->
    <div class="demo-section">
        <h2 class="section-title">データ処理パイプライン</h2>
        
        <div class="demo-group">
            <h3 class="demo-title">4. 複雑なデータ変換</h3>
            <table class="data-table" id="users-table">
                <thead>
                    <tr>
                        <th>名前</th>
                        <th>年齢</th>
                        <th>部署</th>
                        <th>給与</th>
                        <th>都市</th>
                    </tr>
                </thead>
                <tbody id="users-tbody">
                    <!-- 動的生成 -->
                </tbody>
            </table>
            <div class="controls">
                <button class="btn" onclick="processUserData()">データ処理実行</button>
                <button class="btn" onclick="groupByDepartment()">部署別グループ化</button>
                <button class="btn" onclick="calculateStatistics()">統計計算</button>
                <button class="btn btn-secondary" onclick="resetUserData()">データリセット</button>
            </div>
            <div id="pipeline-results"></div>
        </div>
    </div>

    <!-- パフォーマンステスト -->
    <div class="demo-section">
        <h2 class="section-title">パフォーマンステスト</h2>
        
        <div class="demo-group">
            <h3 class="demo-title">5. ネイティブ vs Lodash 比較</h3>
            <div class="controls">
                <button class="btn" onclick="runPerformanceTest()">パフォーマンステスト実行</button>
                <button class="btn btn-secondary" onclick="clearPerformanceResults()">結果クリア</button>
            </div>
            <div class="performance-section" id="performance-results">
                <!-- パフォーマンス結果表示 -->
            </div>
        </div>
    </div>

    <script>
        // グローバル変数
        let debounceCount = 0;
        let throttleCount = 0;
        let userData = [];

        // サンプルデータ生成
        function generateSampleUsers() {
            const departments = ['開発', '営業', '人事', 'マーケティング', '総務'];
            const cities = ['東京', '大阪', '名古屋', '福岡', '札幌'];
            const firstNames = ['太郎', '花子', '次郎', '美咲', '健一', '由美', '宏', '恵子'];
            const lastNames = ['田中', '佐藤', '高橋', '渡辺', '山田', '中村', '小林', '加藤'];
            
            return _.times(20, (i) => ({
                id: i + 1,
                name: _.sample(lastNames) + _.sample(firstNames),
                age: _.random(22, 65),
                department: _.sample(departments),
                salary: _.random(300, 1000) * 1000,
                city: _.sample(cities),
                joinDate: new Date(_.random(2015, 2024), _.random(0, 11), _.random(1, 28))
            }));
        }

        // 配列操作デモ
        function demonstrateArrayMethods() {
            const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 15, 20, 25, 30];
            const users = generateSampleUsers().slice(0, 8);
            
            const code = `
// サンプルデータ
const numbers = [${numbers.join(', ')}];
const users = [/* ユーザーデータ20件 */];

// 1. チャンク（配列を指定サイズに分割）
const chunked = _.chunk(numbers, 3);
// => [[1,2,3], [4,5,6], [7,8,9], [10,15,20], [25,30]]

// 2. 重複除去とソート
const duplicated = [1, 2, 2, 3, 3, 3, 4, 4, 5];
const unique = _.uniq(duplicated);
const sortedDesc = _.orderBy(unique, [], ['desc']);

// 3. 配列の差分・交集合
const arr1 = [1, 2, 3, 4, 5];
const arr2 = [3, 4, 5, 6, 7];
const difference = _.difference(arr1, arr2); // [1, 2]
const intersection = _.intersection(arr1, arr2); // [3, 4, 5]

// 4. 深い平坦化
const nested = [1, [2, [3, [4, [5]]]]];
const flattened = _.flattenDeep(nested); // [1, 2, 3, 4, 5]

// 5. サンプリングとシャッフル
const sample = _.sampleSize(numbers, 5);
const shuffled = _.shuffle(numbers.slice(0, 6));`;

            document.getElementById('array-code').textContent = code;

            const results = [
                { label: 'チャンク（3つずつ）', value: JSON.stringify(_.chunk(numbers, 3)) },
                { label: '重複除去', value: JSON.stringify(_.uniq([1, 2, 2, 3, 3, 3, 4, 4, 5])) },
                { label: '差分', value: JSON.stringify(_.difference([1,2,3,4,5], [3,4,5,6,7])) },
                { label: '交集合', value: JSON.stringify(_.intersection([1,2,3,4,5], [3,4,5,6,7])) },
                { label: '深い平坦化', value: JSON.stringify(_.flattenDeep([1, [2, [3, [4, [5]]]]])) },
                { label: 'ランダムサンプル', value: JSON.stringify(_.sampleSize(numbers, 5)) },
                { label: 'ユーザー名のみ抽出', value: JSON.stringify(_.map(users, 'name').slice(0, 5)) },
                { label: '30歳以上フィルタ', value: `${_.filter(users, u => u.age >= 30).length}人` }
            ];

            displayResults('array-results', results);
        }

        // オブジェクト操作デモ
        function demonstrateObjectMethods() {
            let originalData;
            try {
                originalData = JSON.parse(document.getElementById('object-input').value);
            } catch (e) {
                alert('無効なJSONです。正しい形式で入力してください。');
                return;
            }

            // 深いクローン
            const cloned = _.cloneDeep(originalData);
            cloned.user.name = '変更された名前';
            cloned.user.address.city = '大阪';

            // マージ
            const updates = {
                user: { email: 'new@example.com', age: 31 },
                settings: { language: 'ja' }
            };
            const merged = _.merge(_.cloneDeep(originalData), updates);

            // パス操作
            const name = _.get(originalData, 'user.name');
            const nonExistent = _.get(originalData, 'user.phone', 'デフォルト値');
            
            // オブジェクトのキー・値操作
            const keys = _.keys(originalData);
            const values = _.values(originalData.user);
            const picked = _.pick(originalData.user, ['name', 'age']);
            const omitted = _.omit(originalData.user, ['address']);

            const results = [
                { label: '元データ', value: JSON.stringify(originalData, null, 2) },
                { label: '深いコピー（変更後）', value: JSON.stringify(cloned, null, 2) },
                { label: 'マージ結果', value: JSON.stringify(merged, null, 2) },
                { label: 'パス取得（user.name）', value: name },
                { label: 'デフォルト値付き取得', value: nonExistent },
                { label: 'キー一覧', value: JSON.stringify(keys) },
                { label: 'ピック（name, age）', value: JSON.stringify(picked) },
                { label: 'オミット（address除外）', value: JSON.stringify(omitted) }
            ];

            displayResults('object-results', results);
        }

        // 関数操作デモ初期化
        function setupFunctionMethods() {
            const debouncedFn = _.debounce(() => {
                debounceCount++;
                document.getElementById('debounce-count').textContent = debounceCount;
            }, 500);

            const throttledFn = _.throttle(() => {
                throttleCount++;
                document.getElementById('throttle-count').textContent = throttleCount;
            }, 1000);

            document.getElementById('debounced-btn').addEventListener('click', debouncedFn);
            document.getElementById('throttled-btn').addEventListener('click', throttledFn);
        }

        // データ処理パイプライン
        function processUserData() {
            if (userData.length === 0) {
                userData = generateSampleUsers();
                displayUserTable(userData);
            }

            // 複雑な変換パイプライン
            const processed = _(userData)
                .filter(user => user.age >= 25)
                .map(user => ({
                    ...user,
                    salaryCategory: user.salary >= 600000 ? '高収入' : user.salary >= 400000 ? '中収入' : '一般',
                    experience: new Date().getFullYear() - user.joinDate.getFullYear()
                }))
                .orderBy(['salary'], ['desc'])
                .take(10)
                .value();

            const results = [
                { label: '処理対象件数', value: `${userData.length}件` },
                { label: '25歳以上フィルタ後', value: `${_.filter(userData, u => u.age >= 25).length}件` },
                { label: '平均給与', value: `¥${_.mean(_.map(userData, 'salary')).toLocaleString()}` },
                { label: '最高給与', value: `¥${_.max(_.map(userData, 'salary')).toLocaleString()}` },
                { label: '部署数', value: `${_.uniq(_.map(userData, 'department')).length}部署` },
                { label: 'トップ10（給与順）', value: JSON.stringify(_.map(processed, u => `${u.name}(¥${u.salary.toLocaleString()})`)) }
            ];

            displayResults('pipeline-results', results);
        }

        // 部署別グループ化
        function groupByDepartment() {
            if (userData.length === 0) userData = generateSampleUsers();

            const grouped = _.groupBy(userData, 'department');
            const summary = _.mapValues(grouped, (users, dept) => ({
                count: users.length,
                avgSalary: Math.round(_.mean(_.map(users, 'salary'))),
                avgAge: Math.round(_.mean(_.map(users, 'age')))
            }));

            const results = [
                { label: '部署別サマリー', value: JSON.stringify(summary, null, 2) }
            ];

            displayResults('pipeline-results', results);
        }

        // パフォーマンステスト
        function runPerformanceTest() {
            const testData = _.times(10000, i => ({ id: i, value: Math.random() }));
            const results = [];

            // 配列操作テスト
            const tests = [
                {
                    name: 'Map操作',
                    native: () => testData.map(x => x.value * 2),
                    lodash: () => _.map(testData, x => x.value * 2)
                },
                {
                    name: 'Filter操作', 
                    native: () => testData.filter(x => x.value > 0.5),
                    lodash: () => _.filter(testData, x => x.value > 0.5)
                },
                {
                    name: 'Find操作',
                    native: () => testData.find(x => x.id === 5000),
                    lodash: () => _.find(testData, x => x.id === 5000)
                }
            ];

            tests.forEach(test => {
                const nativeTime = measurePerformance(test.native, 100);
                const lodashTime = measurePerformance(test.lodash, 100);
                
                results.push({
                    name: test.name,
                    nativeTime,
                    lodashTime,
                    winner: nativeTime < lodashTime ? 'Native' : 'Lodash'
                });
            });

            displayPerformanceResults(results);
        }

        // ユーティリティ関数
        function measurePerformance(fn, iterations = 1000) {
            const start = performance.now();
            for (let i = 0; i < iterations; i++) {
                fn();
            }
            return performance.now() - start;
        }

        function displayResults(containerId, results) {
            const container = document.getElementById(containerId);
            container.innerHTML = results.map(result => `
                <div class="result-block">
                    <strong>${result.label}:</strong><br>
                    <span class="highlight">${result.value}</span>
                </div>
            `).join('');
        }

        function displayUserTable(users) {
            const tbody = document.getElementById('users-tbody');
            tbody.innerHTML = users.map(user => `
                <tr>
                    <td>${user.name}</td>
                    <td>${user.age}歳</td>
                    <td>${user.department}</td>
                    <td>¥${user.salary.toLocaleString()}</td>
                    <td>${user.city}</td>
                </tr>
            `).join('');
        }

        function displayPerformanceResults(results) {
            const container = document.getElementById('performance-results');
            container.innerHTML = results.map(result => `
                <div class="perf-item">
                    <div class="perf-title">${result.name}</div>
                    <div class="perf-time">${result.nativeTime.toFixed(2)}</div>
                    <div class="perf-unit">ms (Native)</div>
                    <div class="perf-time">${result.lodashTime.toFixed(2)}</div>
                    <div class="perf-unit">ms (Lodash)</div>
                    <div style="margin-top: 10px; font-weight: bold;">
                        Winner: ${result.winner}
                    </div>
                </div>
            `).join('');
        }

        // クリア・リセット関数群
        function clearArrayResults() {
            document.getElementById('array-results').innerHTML = '';
            document.getElementById('array-code').textContent = '// 実行ボタンを押してコードを確認';
        }

        function resetObjectInput() {
            document.getElementById('object-input').value = `{
  "user": {
    "name": "田中太郎",
    "age": 30,
    "address": {
      "city": "東京",
      "zip": "100-0001"
    }
  },
  "settings": {
    "theme": "dark",
    "notifications": true
  }
}`;
            document.getElementById('object-results').innerHTML = '';
        }

        function resetFunctionCounts() {
            debounceCount = 0;
            throttleCount = 0;
            document.getElementById('debounce-count').textContent = '0';
            document.getElementById('throttle-count').textContent = '0';
        }

        function resetUserData() {
            userData = [];
            document.getElementById('users-tbody').innerHTML = '';
            document.getElementById('pipeline-results').innerHTML = '';
        }

        function clearPerformanceResults() {
            document.getElementById('performance-results').innerHTML = '';
        }

        function calculateStatistics() {
            if (userData.length === 0) userData = generateSampleUsers();

            const stats = {
                totalUsers: userData.length,
                avgAge: _.mean(_.map(userData, 'age')).toFixed(1),
                medianSalary: _.sortBy(userData, 'salary')[Math.floor(userData.length / 2)].salary,
                departmentCounts: _.countBy(userData, 'department'),
                cityCounts: _.countBy(userData, 'city'),
                salaryRange: {
                    min: _.min(_.map(userData, 'salary')),
                    max: _.max(_.map(userData, 'salary'))
                }
            };

            const results = [
                { label: '統計サマリー', value: JSON.stringify(stats, null, 2) }
            ];

            displayResults('pipeline-results', results);
        }

        // 初期化
        document.addEventListener('DOMContentLoaded', function() {
            setupFunctionMethods();
            userData = generateSampleUsers();
            displayUserTable(userData);
            
            console.log('Lodash Version:', _.VERSION);
            console.log('Sample data generated:', userData.length, 'users');
        });
    </script>
</body>
</html>
```

Lodash の実装では、配列操作、オブジェクト操作、関数操作、データ処理パイプライン、パフォーマンステストなど、実際の開発で役立つ包括的な機能を紹介しています。関数型プログラミングのアプローチも含めた実用的な例となっています。

[^20]: Day.js: https://day.js.org/ - Moment.js 軽量代替ライブラリ
[^21]: Lodash: https://lodash.com/ - JavaScript ユーティリティライブラリ

## 5. 専門ライブラリ系CDN（7選）

### 5.1 Three.js 0.179.1 - 3D グラフィックスライブラリ

Three.js[^22]は、WebGL を使用して Web ブラウザで 3D グラフィックスを作成するための最も人気のある JavaScript ライブラリです。複雑な 3D シーンの作成から VR/AR 体験まで、幅広い用途で使用されています。

**特徴**:
- WebGL の複雑性を抽象化
- 豊富な 3D プリミティブ・マテリアル・ライト
- アニメーションシステム内蔵
- VR/AR対応
- パーティクルシステム・ポストエフェクト

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/three@0.179.1/build/three.min.js`
- **cdnjs**: `https://cdnjs.cloudflare.com/ajax/libs/three.js/r179/three.min.js`
- **信頼性スコア**: 9/10
- **ファイルサイズ**: 約 580KB（minified）

**実用デモコード**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Three.js 0.179.1 実用デモ</title>
    <script src="https://cdn.jsdelivr.net/npm/three@0.179.1/build/three.min.js"
            integrity="sha384-gKmQlq+xZdRgQDmIx2IWJQfQjhLQa4BaWNwDJJXNOaFQ4HYF/rZD+8+7l8YgT9sW"
            crossorigin="anonymous"></script>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #000;
            color: white;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            overflow-x: hidden;
        }
        
        .header {
            position: absolute;
            top: 20px;
            left: 20px;
            z-index: 100;
            background: rgba(0,0,0,0.7);
            padding: 20px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }
        
        .title {
            font-size: 2rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .controls {
            position: absolute;
            top: 20px;
            right: 20px;
            z-index: 100;
            background: rgba(0,0,0,0.7);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }
        
        .control-group {
            margin: 10px 0;
        }
        
        .control-label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.9rem;
            color: #ccc;
        }
        
        .control-input {
            width: 100%;
            padding: 5px;
            border: none;
            border-radius: 5px;
            background: rgba(255,255,255,0.1);
            color: white;
        }
        
        .btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            margin: 5px;
            font-size: 12px;
        }
        
        .btn:hover {
            opacity: 0.8;
        }
        
        .stats {
            position: absolute;
            bottom: 20px;
            left: 20px;
            z-index: 100;
            background: rgba(0,0,0,0.7);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            font-family: 'Courier New', monospace;
            font-size: 0.8rem;
        }
        
        .scene-info {
            position: absolute;
            bottom: 20px;
            right: 20px;
            z-index: 100;
            background: rgba(0,0,0,0.7);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            font-size: 0.9rem;
        }
        
        #canvas-container {
            width: 100vw;
            height: 100vh;
        }
        
        .instruction {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            color: rgba(255,255,255,0.7);
            font-size: 1.2rem;
            z-index: 50;
            pointer-events: none;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1 class="title">Three.js 3D デモ</h1>
        <p>インタラクティブ3Dシーンの実装例</p>
    </div>

    <div class="controls">
        <div class="control-group">
            <label class="control-label">アニメーション速度</label>
            <input type="range" class="control-input" id="speed-control" min="0" max="3" step="0.1" value="1">
        </div>
        <div class="control-group">
            <label class="control-label">オブジェクト数</label>
            <input type="range" class="control-input" id="objects-control" min="5" max="50" step="5" value="20">
        </div>
        <div class="control-group">
            <button class="btn" onclick="toggleWireframe()">ワイヤーフレーム</button>
            <button class="btn" onclick="changeColorScheme()">配色変更</button>
        </div>
        <div class="control-group">
            <button class="btn" onclick="addExplosion()">エフェクト</button>
            <button class="btn" onclick="resetScene()">リセット</button>
        </div>
    </div>

    <div class="stats">
        <div>FPS: <span id="fps">0</span></div>
        <div>Objects: <span id="object-count">0</span></div>
        <div>Triangles: <span id="triangle-count">0</span></div>
        <div>Calls: <span id="draw-calls">0</span></div>
    </div>

    <div class="scene-info">
        <div><strong>操作方法</strong></div>
        <div>🖱️ ドラッグ: 回転</div>
        <div>🔍 ホイール: ズーム</div>
        <div>⌨️ キー操作で追加機能</div>
    </div>

    <div class="instruction" id="loading">
        <div>3Dシーンを読み込み中...</div>
    </div>

    <div id="canvas-container"></div>

    <script>
        // Three.js メイン変数
        let scene, camera, renderer, controls;
        let objects = [];
        let particles = [];
        let animationId;
        let isWireframe = false;
        let colorScheme = 0;
        let animationSpeed = 1;
        
        // パフォーマンス測定
        let frameCount = 0;
        let lastTime = Date.now();
        let fps = 0;

        // 3Dシーン初期化
        function initThreeJS() {
            // シーン作成
            scene = new THREE.Scene();
            scene.background = new THREE.Color(0x0a0a0a);
            scene.fog = new THREE.Fog(0x0a0a0a, 10, 50);

            // カメラ設定
            camera = new THREE.PerspectiveCamera(
                75,
                window.innerWidth / window.innerHeight,
                0.1,
                1000
            );
            camera.position.set(15, 15, 15);

            // レンダラー設定
            renderer = new THREE.WebGLRenderer({ 
                antialias: true,
                alpha: true
            });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.shadowMap.enabled = true;
            renderer.shadowMap.type = THREE.PCFSoftShadowMap;
            renderer.outputColorSpace = THREE.SRGBColorSpace;
            
            document.getElementById('canvas-container').appendChild(renderer.domElement);

            // ライト設定
            setupLighting();

            // コントロール設定（簡易版）
            setupControls();

            // 初期オブジェクト作成
            createObjects(20);

            // パーティクルシステム
            createParticleSystem();

            // イベントリスナー
            setupEventListeners();

            // アニメーションループ開始
            animate();

            // ローディング表示を削除
            setTimeout(() => {
                document.getElementById('loading').style.display = 'none';
            }, 1000);
        }

        // ライティング設定
        function setupLighting() {
            // 環境光
            const ambientLight = new THREE.AmbientLight(0x404040, 0.6);
            scene.add(ambientLight);

            // 指向性ライト
            const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
            directionalLight.position.set(20, 20, 20);
            directionalLight.castShadow = true;
            directionalLight.shadow.mapSize.width = 2048;
            directionalLight.shadow.mapSize.height = 2048;
            directionalLight.shadow.camera.near = 0.5;
            directionalLight.shadow.camera.far = 50;
            scene.add(directionalLight);

            // ポイントライト
            const pointLight = new THREE.PointLight(0x4ecdc4, 1, 30);
            pointLight.position.set(10, 10, 10);
            scene.add(pointLight);

            const pointLight2 = new THREE.PointLight(0xff6b6b, 0.8, 25);
            pointLight2.position.set(-10, 5, -10);
            scene.add(pointLight2);
        }

        // 簡易マウスコントロール
        function setupControls() {
            let isDragging = false;
            let previousMousePosition = { x: 0, y: 0 };

            renderer.domElement.addEventListener('mousedown', (event) => {
                isDragging = true;
                previousMousePosition = { x: event.clientX, y: event.clientY };
            });

            window.addEventListener('mousemove', (event) => {
                if (isDragging) {
                    const deltaMove = {
                        x: event.clientX - previousMousePosition.x,
                        y: event.clientY - previousMousePosition.y
                    };

                    const deltaRotationQuaternion = new THREE.Quaternion()
                        .setFromEuler(new THREE.Euler(
                            deltaMove.y * 0.01,
                            deltaMove.x * 0.01,
                            0,
                            'XYZ'
                        ));

                    camera.quaternion.multiplyQuaternions(deltaRotationQuaternion, camera.quaternion);
                    previousMousePosition = { x: event.clientX, y: event.clientY };
                }
            });

            window.addEventListener('mouseup', () => {
                isDragging = false;
            });

            // ズーム
            renderer.domElement.addEventListener('wheel', (event) => {
                event.preventDefault();
                const scale = event.deltaY > 0 ? 1.1 : 0.9;
                camera.position.multiplyScalar(scale);
            });
        }

        // オブジェクト作成
        function createObjects(count) {
            // 既存オブジェクトを削除
            objects.forEach(obj => scene.remove(obj));
            objects = [];

            const geometries = [
                new THREE.BoxGeometry(1, 1, 1),
                new THREE.SphereGeometry(0.6, 16, 16),
                new THREE.ConeGeometry(0.6, 1.2, 8),
                new THREE.CylinderGeometry(0.5, 0.5, 1.2, 16),
                new THREE.TetrahedronGeometry(0.8)
            ];

            for (let i = 0; i < count; i++) {
                const geometry = geometries[Math.floor(Math.random() * geometries.length)];
                const material = new THREE.MeshPhongMaterial({
                    color: getColorSchemeColor(),
                    shininess: 100,
                    wireframe: isWireframe
                });

                const mesh = new THREE.Mesh(geometry, material);
                
                // ランダム配置
                mesh.position.set(
                    (Math.random() - 0.5) * 30,
                    (Math.random() - 0.5) * 20,
                    (Math.random() - 0.5) * 30
                );

                // ランダム回転
                mesh.rotation.set(
                    Math.random() * Math.PI * 2,
                    Math.random() * Math.PI * 2,
                    Math.random() * Math.PI * 2
                );

                // カスタムプロパティ
                mesh.userData = {
                    initialPosition: mesh.position.clone(),
                    rotationSpeed: {
                        x: (Math.random() - 0.5) * 0.02,
                        y: (Math.random() - 0.5) * 0.02,
                        z: (Math.random() - 0.5) * 0.02
                    },
                    floatAmplitude: Math.random() * 2 + 1,
                    floatSpeed: Math.random() * 0.02 + 0.01
                };

                mesh.castShadow = true;
                mesh.receiveShadow = true;

                scene.add(mesh);
                objects.push(mesh);
            }
        }

        // パーティクルシステム
        function createParticleSystem() {
            const particleCount = 1000;
            const geometry = new THREE.BufferGeometry();
            const positions = new Float32Array(particleCount * 3);
            const colors = new Float32Array(particleCount * 3);

            for (let i = 0; i < particleCount * 3; i += 3) {
                positions[i] = (Math.random() - 0.5) * 100;
                positions[i + 1] = (Math.random() - 0.5) * 100;
                positions[i + 2] = (Math.random() - 0.5) * 100;

                const color = new THREE.Color(getColorSchemeColor());
                colors[i] = color.r;
                colors[i + 1] = color.g;
                colors[i + 2] = color.b;
            }

            geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
            geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));

            const material = new THREE.PointsMaterial({
                size: 0.1,
                vertexColors: true,
                transparent: true,
                opacity: 0.6
            });

            const particleSystem = new THREE.Points(geometry, material);
            scene.add(particleSystem);
            particles.push(particleSystem);
        }

        // 配色取得
        function getColorSchemeColor() {
            const schemes = [
                [0xff6b6b, 0x4ecdc4, 0x45b7d1, 0x96c93d, 0xfeca57],
                [0x667eea, 0x764ba2, 0xf093fb, 0xf5576c, 0x4facfe],
                [0xff9a9e, 0xfecfef, 0xfecfef, 0xa8e6cf, 0xdcedc8]
            ];
            
            const currentScheme = schemes[colorScheme % schemes.length];
            return currentScheme[Math.floor(Math.random() * currentScheme.length)];
        }

        // アニメーションループ
        function animate() {
            animationId = requestAnimationFrame(animate);

            // FPS計算
            frameCount++;
            const currentTime = Date.now();
            if (currentTime - lastTime >= 1000) {
                fps = Math.round((frameCount * 1000) / (currentTime - lastTime));
                frameCount = 0;
                lastTime = currentTime;
                updateStats();
            }

            // オブジェクトアニメーション
            const time = Date.now() * 0.001 * animationSpeed;
            
            objects.forEach((obj, index) => {
                // 回転
                obj.rotation.x += obj.userData.rotationSpeed.x * animationSpeed;
                obj.rotation.y += obj.userData.rotationSpeed.y * animationSpeed;
                obj.rotation.z += obj.userData.rotationSpeed.z * animationSpeed;

                // 浮遊
                obj.position.y = obj.userData.initialPosition.y + 
                    Math.sin(time * obj.userData.floatSpeed + index) * obj.userData.floatAmplitude;

                // 軌道運動
                const radius = 5;
                const orbitSpeed = 0.5;
                obj.position.x = obj.userData.initialPosition.x + 
                    Math.cos(time * orbitSpeed + index) * radius;
                obj.position.z = obj.userData.initialPosition.z + 
                    Math.sin(time * orbitSpeed + index) * radius;
            });

            // パーティクル回転
            particles.forEach(particle => {
                particle.rotation.y += 0.001 * animationSpeed;
            });

            // カメラの自動回転（微細）
            camera.position.x = Math.cos(time * 0.1) * 0.5 + camera.position.x * 0.99;
            camera.lookAt(scene.position);

            renderer.render(scene, camera);
        }

        // 統計更新
        function updateStats() {
            document.getElementById('fps').textContent = fps;
            document.getElementById('object-count').textContent = objects.length;
            document.getElementById('triangle-count').textContent = (objects.length * 12).toLocaleString(); // 概算
            document.getElementById('draw-calls').textContent = objects.length + particles.length;
        }

        // イベントリスナー設定
        function setupEventListeners() {
            // ウィンドウリサイズ
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });

            // コントロール
            document.getElementById('speed-control').addEventListener('input', (e) => {
                animationSpeed = parseFloat(e.target.value);
            });

            document.getElementById('objects-control').addEventListener('input', (e) => {
                createObjects(parseInt(e.target.value));
            });

            // キーボードイベント
            window.addEventListener('keydown', (event) => {
                switch(event.code) {
                    case 'Space':
                        event.preventDefault();
                        addExplosion();
                        break;
                    case 'KeyR':
                        resetScene();
                        break;
                    case 'KeyW':
                        toggleWireframe();
                        break;
                    case 'KeyC':
                        changeColorScheme();
                        break;
                }
            });
        }

        // インタラクティブ機能
        function toggleWireframe() {
            isWireframe = !isWireframe;
            objects.forEach(obj => {
                obj.material.wireframe = isWireframe;
            });
        }

        function changeColorScheme() {
            colorScheme++;
            objects.forEach(obj => {
                obj.material.color.setHex(getColorSchemeColor());
            });
            
            // パーティクル再生成
            scene.remove(particles[0]);
            particles = [];
            createParticleSystem();
        }

        function addExplosion() {
            // 爆発エフェクト（簡易版）
            const explosionGeometry = new THREE.SphereGeometry(0.1, 8, 8);
            const explosionMaterial = new THREE.MeshBasicMaterial({
                color: 0xffff00,
                transparent: true,
                opacity: 0.8
            });

            for (let i = 0; i < 20; i++) {
                const explosion = new THREE.Mesh(explosionGeometry, explosionMaterial.clone());
                explosion.position.set(
                    (Math.random() - 0.5) * 10,
                    (Math.random() - 0.5) * 10,
                    (Math.random() - 0.5) * 10
                );

                const scale = Math.random() * 2 + 1;
                explosion.scale.set(scale, scale, scale);

                scene.add(explosion);

                // フェードアウト
                const fadeOut = () => {
                    explosion.material.opacity -= 0.02;
                    explosion.scale.multiplyScalar(1.05);
                    
                    if (explosion.material.opacity > 0) {
                        requestAnimationFrame(fadeOut);
                    } else {
                        scene.remove(explosion);
                        explosion.geometry.dispose();
                        explosion.material.dispose();
                    }
                };
                
                setTimeout(fadeOut, i * 50);
            }
        }

        function resetScene() {
            // シーンリセット
            createObjects(20);
            animationSpeed = 1;
            document.getElementById('speed-control').value = 1;
            document.getElementById('objects-control').value = 20;
            
            camera.position.set(15, 15, 15);
            camera.lookAt(scene.position);
        }

        // 初期化実行
        window.addEventListener('load', () => {
            initThreeJS();
            console.log('Three.js Version:', THREE.REVISION);
            console.log('WebGL Supported:', !!renderer.getContext());
        });

        // メモリクリーンアップ
        window.addEventListener('beforeunload', () => {
            if (animationId) {
                cancelAnimationFrame(animationId);
            }
            
            objects.forEach(obj => {
                obj.geometry.dispose();
                obj.material.dispose();
            });
            
            particles.forEach(particle => {
                particle.geometry.dispose();
                particle.material.dispose();
            });
            
            renderer.dispose();
        });
    </script>
</body>
</html>
```

Three.js の実装では、インタラクティブな 3D シーン、リアルタイムアニメーション、パーティクルシステム、エフェクトなどの機能を含む包括的な例を提供しています。WebGL の複雑性を抽象化しつつ、実用的な 3D Web アプリケーションの基盤となる実装です。

### 5.2 Prism.js 1系 - シンタックスハイライト

Prism.js[^23]は、軽量でカスタマイズ可能なシンタックスハイライトライブラリです。280以上のプログラミング言語をサポートし、プラグインシステムにより機能拡張が可能です。

**特徴**:
- 280以上の言語サポート
- 豊富なテーマ（8種類のデフォルトテーマ）
- プラグインシステム
- 行番号・行ハイライト機能
- 軽量設計（2KB～）

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/prismjs@1.29.0/components/prism-core.min.js`
- **Prism CSS**: `https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism.min.css`
- **信頼性スコア**: 9/10
- **ファイルサイズ**: 約 2KB（コア）+ 言語別追加

**実用デモコード**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prism.js 1.29.0 実用デモ</title>
    
    <!-- Prism.js CSS - 複数テーマを動的切り替えするため複数読み込み -->
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism.min.css" rel="stylesheet" id="prism-theme-default">
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism-dark.min.css" rel="stylesheet" id="prism-theme-dark" disabled>
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism-funky.min.css" rel="stylesheet" id="prism-theme-funky" disabled>
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism-okaidia.min.css" rel="stylesheet" id="prism-theme-okaidia" disabled>
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism-twilight.min.css" rel="stylesheet" id="prism-theme-twilight" disabled>
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism-coy.min.css" rel="stylesheet" id="prism-theme-coy" disabled>
    
    <!-- Prism.js コアとプラグイン -->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/components/prism-core.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/autoloader/prism-autoloader.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/line-numbers/prism-line-numbers.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/line-highlight/prism-line-highlight.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/copy-to-clipboard/prism-copy-to-clipboard.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/toolbar/prism-toolbar.min.js"></script>
    
    <!-- プラグイン用CSS -->
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/line-numbers/prism-line-numbers.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/line-highlight/prism-line-highlight.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/plugins/toolbar/prism-toolbar.min.css" rel="stylesheet">
    
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #2d3436 0%, #636e72 100%);
            min-height: 100vh;
            color: white;
        }
        
        .header {
            text-align: center;
            margin-bottom: 40px;
            background: rgba(255,255,255,0.1);
            padding: 30px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
        }
        
        .main-title {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #74b9ff, #0984e3);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .demo-section {
            background: rgba(255,255,255,0.05);
            border-radius: 15px;
            padding: 30px;
            margin: 30px 0;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 25px;
            color: #74b9ff;
            border-bottom: 2px solid #74b9ff;
            padding-bottom: 10px;
        }
        
        .controls {
            margin: 25px 0;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            align-items: center;
        }
        
        .control-group {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(255,255,255,0.1);
            padding: 10px 15px;
            border-radius: 8px;
        }
        
        .control-label {
            font-size: 0.9rem;
            color: #ddd;
            white-space: nowrap;
        }
        
        .control-select {
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            background: rgba(255,255,255,0.2);
            color: white;
            cursor: pointer;
        }
        
        .control-select option {
            background: #2d3436;
            color: white;
        }
        
        .btn {
            background: linear-gradient(45deg, #74b9ff, #0984e3);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            transition: transform 0.2s;
        }
        
        .btn:hover {
            transform: translateY(-2px);
        }
        
        .btn-secondary {
            background: linear-gradient(45deg, #636e72, #2d3436);
        }
        
        .editor-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin: 25px 0;
            height: 500px;
        }
        
        .editor-panel {
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            overflow: hidden;
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .panel-header {
            background: rgba(116, 185, 255, 0.2);
            padding: 15px;
            font-weight: 600;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .code-input {
            width: 100%;
            height: calc(100% - 60px);
            background: transparent;
            color: white;
            border: none;
            padding: 20px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            resize: none;
            outline: none;
        }
        
        .preview-panel {
            padding: 20px;
            overflow-y: auto;
            height: calc(100% - 60px);
        }
        
        .language-showcase {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }
        
        .showcase-item {
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            overflow: hidden;
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .showcase-header {
            background: rgba(116, 185, 255, 0.2);
            padding: 15px;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .language-badge {
            background: rgba(255,255,255,0.2);
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.8rem;
        }
        
        /* Prismコード表示の調整 */
        .showcase-item pre {
            margin: 0;
            background: transparent !important;
        }
        
        .showcase-item code {
            font-size: 13px !important;
            line-height: 1.5 !important;
        }
        
        .stats-panel {
            background: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 10px;
            margin: 25px 0;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        
        .stat-item {
            background: rgba(116, 185, 255, 0.2);
            padding: 20px;
            border-radius: 8px;
            text-align: center;
        }
        
        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #74b9ff;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .feature-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 15px;
            margin: 25px 0;
        }
        
        .feature-item {
            background: rgba(255,255,255,0.05);
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #74b9ff;
        }
        
        .feature-title {
            font-weight: 600;
            color: #74b9ff;
            margin-bottom: 10px;
        }
        
        .feature-desc {
            font-size: 0.9rem;
            opacity: 0.8;
            line-height: 1.5;
        }
        
        @media (max-width: 768px) {
            .editor-container {
                grid-template-columns: 1fr;
                height: auto;
            }
            
            .language-showcase {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1 class="main-title">Prism.js 実用デモ</h1>
        <p class="subtitle">280以上の言語対応シンタックスハイライトライブラリ</p>
    </div>

    <!-- コントロールパネル -->
    <div class="demo-section">
        <h2 class="section-title">設定コントロール</h2>
        <div class="controls">
            <div class="control-group">
                <span class="control-label">テーマ:</span>
                <select class="control-select" id="theme-select">
                    <option value="default">Default</option>
                    <option value="dark">Dark</option>
                    <option value="funky">Funky</option>
                    <option value="okaidia">Okaidia</option>
                    <option value="twilight">Twilight</option>
                    <option value="coy">Coy</option>
                </select>
            </div>
            <div class="control-group">
                <span class="control-label">言語:</span>
                <select class="control-select" id="language-select">
                    <option value="javascript">JavaScript</option>
                    <option value="python">Python</option>
                    <option value="java">Java</option>
                    <option value="cpp">C++</option>
                    <option value="php">PHP</option>
                    <option value="go">Go</option>
                    <option value="rust">Rust</option>
                    <option value="typescript">TypeScript</option>
                </select>
            </div>
            <button class="btn" onclick="toggleLineNumbers()">行番号切替</button>
            <button class="btn" onclick="highlightRandomLine()">行ハイライト</button>
            <button class="btn btn-secondary" onclick="resetEditor()">リセット</button>
        </div>
    </div>

    <!-- ライブエディター -->
    <div class="demo-section">
        <h2 class="section-title">ライブエディター</h2>
        <div class="editor-container">
            <div class="editor-panel">
                <div class="panel-header">コード入力</div>
                <textarea class="code-input" id="code-input" placeholder="ここにコードを入力してください...">// JavaScript のサンプルコード
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// 配列の操作
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(x => x * 2);
const evens = numbers.filter(x => x % 2 === 0);

// 非同期処理
async function fetchUserData(userId) {
    try {
        const response = await fetch(\`/api/users/\${userId}\`);
        const userData = await response.json();
        return userData;
    } catch (error) {
        console.error('Error fetching user data:', error);
        throw error;
    }
}

// クラス定義
class Calculator {
    constructor() {
        this.history = [];
    }
    
    add(a, b) {
        const result = a + b;
        this.history.push(\`\${a} + \${b} = \${result}\`);
        return result;
    }
    
    getHistory() {
        return this.history;
    }
}

console.log('Prism.js デモ開始');
</textarea>
            </div>
            <div class="editor-panel">
                <div class="panel-header">プレビュー</div>
                <div class="preview-panel">
                    <pre class="line-numbers" data-line="1,5-7"><code id="preview-code" class="language-javascript"></code></pre>
                </div>
            </div>
        </div>
    </div>

    <!-- 言語ショーケース -->
    <div class="demo-section">
        <h2 class="section-title">多言語対応ショーケース</h2>
        <div class="language-showcase" id="language-showcase">
            <!-- 動的に生成 -->
        </div>
    </div>

    <!-- 機能紹介 -->
    <div class="demo-section">
        <h2 class="section-title">主要機能</h2>
        <div class="feature-list">
            <div class="feature-item">
                <div class="feature-title">🎨 豊富なテーマ</div>
                <div class="feature-desc">8種類のデフォルトテーマに加え、カスタムテーマも簡単に作成可能</div>
            </div>
            <div class="feature-item">
                <div class="feature-title">🔢 行番号表示</div>
                <div class="feature-desc">プラグインにより行番号の表示・非表示を切り替え可能</div>
            </div>
            <div class="feature-item">
                <div class="feature-title">📋 コピー機能</div>
                <div class="feature-desc">ワンクリックでコードをクリップボードにコピー</div>
            </div>
            <div class="feature-item">
                <div class="feature-title">🎯 行ハイライト</div>
                <div class="feature-desc">特定の行を強調表示して重要な部分を際立たせる</div>
            </div>
            <div class="feature-item">
                <div class="feature-title">🚀 軽量設計</div>
                <div class="feature-desc">必要な言語のみを読み込み、最小限のサイズでパフォーマンス最適化</div>
            </div>
            <div class="feature-item">
                <div class="feature-title">🔧 プラグイン拡張</div>
                <div class="feature-desc">豊富なプラグインエコシステムで機能を自由に拡張</div>
            </div>
        </div>
    </div>

    <!-- 統計パネル -->
    <div class="demo-section">
        <h2 class="section-title">Prism.js 統計情報</h2>
        <div class="stats-panel">
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-number" id="supported-languages">280+</div>
                    <div class="stat-label">対応言語数</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="theme-count">8</div>
                    <div class="stat-label">デフォルトテーマ</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="plugin-count">20+</div>
                    <div class="stat-label">公式プラグイン</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="file-size">2KB</div>
                    <div class="stat-label">コアサイズ</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // サンプルコード集
        const sampleCodes = {
            javascript: {
                code: `// JavaScript のサンプルコード
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(x => x * 2);

// 非同期処理
async function fetchData(url) {
    const response = await fetch(url);
    return response.json();
}

class Calculator {
    constructor() {
        this.history = [];
    }
    
    add(a, b) {
        return a + b;
    }
}`,
                title: 'JavaScript / ES6+',
                description: 'モダンJavaScriptの機能を含む完全対応'
            },
            python: {
                code: `# Python のサンプルコード
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

# リスト内包表記
numbers = [1, 2, 3, 4, 5]
doubled = [x * 2 for x in numbers]
evens = [x for x in numbers if x % 2 == 0]

# クラス定義
class Calculator:
    def __init__(self):
        self.history = []
    
    def add(self, a, b):
        result = a + b
        self.history.append(f"{a} + {b} = {result}")
        return result
    
    def get_history(self):
        return self.history

# デコレータ
def measure_time(func):
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f} seconds")
        return result
    return wrapper`,
                title: 'Python 3',
                description: 'Pythonの全ての構文をサポート'
            },
            java: {
                code: `// Java のサンプルコード
public class Calculator {
    private List<String> history;
    
    public Calculator() {
        this.history = new ArrayList<>();
    }
    
    public int add(int a, int b) {
        int result = a + b;
        history.add(String.format("%d + %d = %d", a, b, result));
        return result;
    }
    
    public List<String> getHistory() {
        return new ArrayList<>(history);
    }
}

// ストリーム API
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> doubled = numbers.stream()
    .map(x -> x * 2)
    .collect(Collectors.toList());

// ラムダ式
Comparator<String> lengthComparator = 
    (s1, s2) -> Integer.compare(s1.length(), s2.length());`,
                title: 'Java 8+',
                description: 'モダンJava機能も完全サポート'
            },
            cpp: {
                code: `// C++ のサンプルコード
#include <iostream>
#include <vector>
#include <algorithm>
#include <memory>

template<typename T>
class Calculator {
private:
    std::vector<T> history;
    
public:
    Calculator() = default;
    
    T add(T a, T b) {
        T result = a + b;
        history.push_back(result);
        return result;
    }
    
    const std::vector<T>& getHistory() const {
        return history;
    }
};

// ラムダ式とアルゴリズム
int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    
    // ラムダ式を使用した変換
    std::transform(numbers.begin(), numbers.end(), 
                   numbers.begin(), [](int x) { return x * 2; });
    
    // スマートポインタ
    auto calc = std::make_unique<Calculator<int>>();
    calc->add(10, 20);
    
    return 0;
}`,
                title: 'C++ 17/20',
                description: 'モダンC++機能を含む完全対応'
            }
        };

        let currentLanguage = 'javascript';
        let currentTheme = 'default';
        let lineNumbersEnabled = true;

        // 初期化
        document.addEventListener('DOMContentLoaded', function() {
            // Prism autoloader 設定
            Prism.plugins.autoloader.languages_path = 'https://cdn.jsdelivr.net/npm/prismjs@1.29.0/components/';
            
            // ライブエディター初期化
            updatePreview();
            createLanguageShowcase();
            
            // イベントリスナー設定
            setupEventListeners();
            
            console.log('Prism.js Version:', '1.29.0');
            console.log('Supported Languages:', Object.keys(Prism.languages).length);
        });

        // イベントリスナー設定
        function setupEventListeners() {
            document.getElementById('code-input').addEventListener('input', updatePreview);
            document.getElementById('theme-select').addEventListener('change', changeTheme);
            document.getElementById('language-select').addEventListener('change', changeLanguage);
        }

        // プレビュー更新
        function updatePreview() {
            const code = document.getElementById('code-input').value;
            const previewCode = document.getElementById('preview-code');
            
            previewCode.textContent = code;
            previewCode.className = `language-${currentLanguage}`;
            
            // 親要素のクラスも更新
            const preElement = previewCode.parentElement;
            preElement.className = lineNumbersEnabled ? 'line-numbers' : '';
            
            // Prismでハイライト
            Prism.highlightElement(previewCode);
        }

        // テーマ変更
        function changeTheme() {
            const newTheme = document.getElementById('theme-select').value;
            
            // 全テーマを無効化
            document.querySelectorAll('[id^="prism-theme-"]').forEach(link => {
                link.disabled = true;
            });
            
            // 選択されたテーマを有効化
            document.getElementById(`prism-theme-${newTheme}`).disabled = false;
            currentTheme = newTheme;
            
            // ショーケースも再ハイライト
            setTimeout(recreateShowcase, 100);
        }

        // 言語変更
        function changeLanguage() {
            const newLanguage = document.getElementById('language-select').value;
            currentLanguage = newLanguage;
            
            // サンプルコードがあれば更新
            if (sampleCodes[newLanguage]) {
                document.getElementById('code-input').value = sampleCodes[newLanguage].code;
            }
            
            updatePreview();
        }

        // 行番号切替
        function toggleLineNumbers() {
            lineNumbersEnabled = !lineNumbersEnabled;
            updatePreview();
            recreateShowcase();
        }

        // ランダム行ハイライト
        function highlightRandomLine() {
            const codeLines = document.getElementById('code-input').value.split('\n').length;
            const randomLine = Math.floor(Math.random() * Math.min(codeLines, 10)) + 1;
            const randomRange = randomLine + '-' + (randomLine + 2);
            
            const preElement = document.querySelector('#preview-code').parentElement;
            preElement.setAttribute('data-line', randomRange);
            
            // 再ハイライト
            updatePreview();
        }

        // エディターリセット
        function resetEditor() {
            document.getElementById('code-input').value = sampleCodes.javascript.code;
            document.getElementById('language-select').value = 'javascript';
            document.getElementById('theme-select').value = 'default';
            
            currentLanguage = 'javascript';
            currentTheme = 'default';
            lineNumbersEnabled = true;
            
            changeTheme();
            updatePreview();
        }

        // 言語ショーケース作成
        function createLanguageShowcase() {
            const showcase = document.getElementById('language-showcase');
            showcase.innerHTML = '';
            
            Object.entries(sampleCodes).forEach(([lang, data]) => {
                const item = document.createElement('div');
                item.className = 'showcase-item';
                
                const uniqueId = `code-${lang}-${Date.now()}`;
                
                item.innerHTML = `
                    <div class="showcase-header">
                        <span>${data.title}</span>
                        <span class="language-badge">${lang}</span>
                    </div>
                    <pre ${lineNumbersEnabled ? 'class="line-numbers"' : ''}><code id="${uniqueId}" class="language-${lang}">${data.code}</code></pre>
                `;
                
                showcase.appendChild(item);
                
                // ハイライト適用
                setTimeout(() => {
                    const codeElement = document.getElementById(uniqueId);
                    if (codeElement) {
                        Prism.highlightElement(codeElement);
                    }
                }, 50);
            });
        }

        // ショーケース再作成
        function recreateShowcase() {
            createLanguageShowcase();
        }

        // 統計情報更新（動的に）
        function updateStats() {
            // 実際の値（簡略化）
            document.getElementById('supported-languages').textContent = '280+';
            document.getElementById('theme-count').textContent = '8';
            document.getElementById('plugin-count').textContent = '20+';
            document.getElementById('file-size').textContent = '2KB';
        }

        // 初期統計更新
        setTimeout(updateStats, 1000);
    </script>
</body>
</html>
```

Prism.js の実装では、リアルタイムシンタックスハイライト、テーマ切り替え、多言語対応、プラグイン活用など、実用的なコードエディターの基盤となる機能を提供しています。

[^22]: Three.js: https://threejs.org/ - WebGL 3D ライブラリ
[^23]: Prism.js: https://prismjs.com/ - シンタックスハイライトライブラリ

### 5.3 D3.js 7系 - データビジュアライゼーション

D3.js[^24]は、データドリブンなドキュメント操作のための JavaScript ライブラリです。SVG、Canvas、HTML を活用し、複雑なデータビジュアライゼーションを作成できます。

**特徴**:
- データバインディング
- SVG/Canvas対応  
- 豊富なスケール・軸・レイアウト
- アニメーション・インタラクション
- モジュラー設計

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/d3@7.9.0/dist/d3.min.js`
- **信頼性スコア**: 10/10
- **ファイルサイズ**: 約 270KB（minified）

### 5.4 Moment.js 2系 - レガシー日時ライブラリ（参考）

Moment.js[^25]は長年使われてきた日時処理ライブラリですが、現在はメンテナンスモードです。新規プロジェクトでは Day.js や date-fns の使用が推奨されています。

**特徴**:
- 豊富な日時操作機能
- 多言語対応
- タイムゾーン処理
- ⚠️ メンテナンスモード
- 大きなファイルサイズ

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/moment@2.30.1/min/moment.min.js`
- **信頼性スコア**: 7/10（レガシー）
- **ファイルサイズ**: 約 67KB（minified）

### 5.5 Underscore.js 1.13系 - 関数型プログラミング支援

Underscore.js[^26]は JavaScript の関数型プログラミングを支援するユーティリティライブラリです。Lodash のベースとなったライブラリで、現在も軽量な選択肢として使用されます。

**特徴**:
- 関数型プログラミング支援
- 100以上のユーティリティ関数
- Lodash より軽量
- 依存関係なし
- ES6+ 機能との共存

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/underscore@1.13.6/underscore-umd-min.js`
- **信頼性スコア**: 8/10
- **ファイルサイズ**: 約 25KB（minified）

### 5.6 Materialize CSS 1系 - Material Design CSSフレームワーク

Materialize[^27]は、Google の Material Design 原則に基づいた CSS フレームワークです。モバイルファーストのレスポンシブ設計が特徴です。

**特徴**:
- Material Design 準拠
- レスポンシブグリッドシステム
- 豊富なコンポーネント
- JavaScript プラグイン内蔵
- Sass 対応

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/materialize-css@1.0.0/dist/css/materialize.min.css`
- **Materialize JS**: `https://cdn.jsdelivr.net/npm/materialize-css@1.0.0/dist/js/materialize.min.js`
- **信頼性スコア**: 7/10
- **ファイルサイズ**: 約 130KB（CSS + JS）

### 5.7 Particles.js - パーティクルアニメーション

Particles.js[^28]は、Web サイトの背景に美しいパーティクルアニメーションを追加するための軽量ライブラリです。カスタマイズ性が高く、パフォーマンスに配慮した実装が特徴です。

**特徴**:
- 軽量設計（20KB以下）
- 高度なカスタマイズ性
- レスポンシブ対応
- Canvas ベース描画
- TypeScript対応

**CDN情報**  
- **jsDelivr**: `https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js`
- **信頼性スコア**: 8/10
- **ファイルサイズ**: 約 15KB（minified）

## 6. 実践的な活用方法

### 6.1 組み合わせのベストプラクティス

**基本的な組み合わせパターン**

```html
<!-- パフォーマンス重視の軽量構成 -->
<link href="https://cdn.jsdelivr.net/npm/tailwindcss@3.4.1/dist/tailwind.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/alpine.js@3.14.1/dist/cdn.min.js" defer></script>
<script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/dayjs.min.js"></script>

<!-- 本格的なWebアプリ構成 -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>

<!-- データビジュアライゼーション特化構成 -->
<script src="https://cdn.jsdelivr.net/npm/d3@7.9.0/dist/d3.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.179.1/build/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
```

**CDN選択の指針**

| プロジェクト種別 | 推奨CDN構成 | 理由 |
|------------|-----------|-----|
| プロトタイピング | jsDelivr + 基本ライブラリ | 迅速な開発開始 |
| 企業サイト | cdnjs + Bootstrap + jQuery | 安定性・信頼性重視 |
| SPA開発 | unpkg + モダンライブラリ | 最新機能の活用 |
| パフォーマンス重視 | 複数CDN + SRI | 冗長性とセキュリティ |

### 6.2 パフォーマンス最適化のコツ

**1. 必要最小限のライブラリ選択**
```html
<!-- ❌ 悪い例：不要に重いライブラリ -->
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
<!-- 簡単な配列操作のためだけに70KBは過剰 -->

<!-- ✅ 良い例：必要な機能のみ -->
<script src="https://cdn.jsdelivr.net/npm/lodash.map@4.6.0/index.js"></script>
<!-- 特定の機能のみをインポート -->
```

**2. CDN の適切な設定**
```html
<!-- DNS プリフェッチでCDN接続を高速化 -->
<link rel="dns-prefetch" href="//cdn.jsdelivr.net">
<link rel="dns-prefetch" href="//cdnjs.cloudflare.com">

<!-- 重要でないリソースの遅延読み込み -->
<script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js" defer></script>

<!-- SRIハッシュによるセキュリティ確保 -->
<script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.10/dayjs.min.js" 
        integrity="sha384-fww6xHa6+AKBwEK5ZOxfyCAONrU/w6xIm1nGUw6TlZKrMWKgvmOmBsP3mNY5W1yf" 
        crossorigin="anonymous"></script>
```

**3. フォールバック戦略**
```javascript
// CDN読み込み失敗時のローカルフォールバック
function loadFallback(src, test, callback) {
    const script = document.createElement('script');
    script.src = src;
    script.onload = function() {
        if (test()) {
            callback();
        } else {
            loadFallback('/js/local-fallback.js', test, callback);
        }
    };
    script.onerror = function() {
        loadFallback('/js/local-fallback.js', test, callback);
    };
    document.head.appendChild(script);
}

// 使用例
loadFallback(
    'https://cdn.jsdelivr.net/npm/jquery@3.7.1/dist/jquery.min.js',
    () => typeof jQuery !== 'undefined',
    () => console.log('jQuery loaded successfully')
);
```

### 6.3 トラブルシューティング

**よくある問題と解決策**

| 問題 | 原因 | 解決策 |
|------|------|--------|
| スクリプト読み込み失敗 | CDN障害、ネットワーク問題 | フォールバック実装 |
| スタイル崩れ | CSS読み込み順序、バージョン競合 | 読み込み順序の見直し |
| パフォーマンス低下 | 不要なライブラリ、重複読み込み | ライブラリの精査・統合 |
| セキュリティ警告 | SRI未設定、HTTPSでない | HTTPS化、SRI追加 |

**デバッグのためのコンソール確認**
```javascript
// 読み込み確認用のデバッグコード
console.log('=== ライブラリ読み込み確認 ===');
console.log('jQuery:', typeof jQuery !== 'undefined' ? jQuery.fn.jquery : '未読み込み');
console.log('Bootstrap:', typeof bootstrap !== 'undefined' ? '読み込み済み' : '未読み込み');
console.log('Chart.js:', typeof Chart !== 'undefined' ? Chart.version : '未読み込み');
console.log('Day.js:', typeof dayjs !== 'undefined' ? dayjs.version : '未読み込み');
console.log('Three.js:', typeof THREE !== 'undefined' ? THREE.REVISION : '未読み込み');
```

## 7. まとめ

### CDN活用による開発効率の向上

2025年現在、単一HTMLドキュメント開発において CDN は不可欠な技術基盤となっています。本記事で紹介した20選のライブラリは、以下の基準で厳選されています：

- **信頼性**: 継続的なメンテナンスと豊富な実績
- **パフォーマンス**: 最適化された配信とキャッシュ戦略
- **互換性**: 最新ブラウザから旧バージョンまでの幅広い対応
- **実用性**: 実際の開発現場での活用価値

### 2025年以降のトレンド展望

**技術トレンド**
- **ESM対応の加速**: ES Modules による効率的な読み込み
- **HTTP/3の普及**: より高速なCDN配信の実現
- **エッジコンピューティング**: レスポンス時間のさらなる短縮
- **TypeScript標準化**: 型安全性を重視した開発の浸透

**開発手法の進化**
- **マイクロフロントエンド**: 小さな機能単位での開発
- **ゼロバンドル開発**: ビルドプロセスの簡略化
- **プログレッシブエンハンスメント**: 段階的な機能向上アプローチ

### 推奨事項

1. **プロジェクト特性に応じた選択**: 要件に最適なライブラリ組み合わせを選択
2. **継続的な最新化**: セキュリティと機能向上のための定期更新
3. **パフォーマンス監視**: Core Web Vitals を指標とした最適化
4. **フォールバック戦略**: CDN 障害に備えた冗長性の確保

単一HTML開発は、適切なCDN活用により、従来のビルドプロセスを必要とする開発手法と遜色ない、高機能で実用的なWebアプリケーション構築を可能にします。本記事で紹介したライブラリとベストプラクティスを活用し、効率的で持続可能な Web 開発を実現してください。

[^24]: D3.js: https://d3js.org/ - データビジュアライゼーションライブラリ
[^25]: Moment.js: https://momentjs.com/ - 日時処理ライブラリ（メンテナンスモード）
[^26]: Underscore.js: https://underscorejs.org/ - 関数型プログラミング支援
[^27]: Materialize: https://materializecss.com/ - Material Design フレームワーク
[^28]: Particles.js: https://vincentgarreau.com/particles.js/ - パーティクルアニメーション記事執筆完了 - Fri, Aug 22, 2025 11:55:07 PM
