---
permalink: /llm-drawio-xml-diagram-automation-guide
title: "LLMでdraw.io XMLを書いてシステム図を爆速生成 - Claude 3.7 + IaC連携の完全ガイド"
summary: "draw.ioのXML構造を理解し、Claude 3.7 Sonnetでシステム構成図・フロー図・組織図を自動生成する実践ガイド。Terraform/CDK連携、プロンプトテンプレート、トラブルシューティングまで網羅。"
tags:
  - "#draw-io"
  - "#llm"
  - "#claude-sonnet-3-7"
  - "#diagram-automation"
  - "#iac"
  - "#mxgraph"
  - "#aws-architecture"
  - "#prompt-engineering"
  - "#devops"
  - "#infrastructure-as-code"
---

## 1. なぜ今「LLM × draw.io XML」なのか

システム開発において、構成図やフローチャートの作成は避けて通れない作業である。しかし従来のGUI作図は多くの課題を抱えている。マウスで図形を配置し、線を引き、整列させる作業に何時間もかかる。さらに深刻なのは、TerraformやCDKで構築したインフラと手動メンテナンスの図表が常に乖離してしまう点だ[18]。設計変更のたびに複数の図を手直しする労力は、開発生産性の大きな足かせとなっている。

こうした課題に対し、draw.io（diagrams.net）のXMLベースという特性とLLM（Large Language Model）の進化が新たな解決策を提示している。draw.ioはmxGraphライブラリをベースとしたXML形式で図表を定義するため[1]、バージョン管理、自動生成、API連携が容易である。さらにClaude 3.7 Sonnetをはじめとする最新LLMは、mxGraph XMLスキーマの学習精度が飛躍的に向上し、実用的な図表を生成できるレベルに到達している[3]。

2025年時点では、「プロンプト1回でAWS構成図が完成」「IaCコードから構成図を自動生成」といった実務シナリオが現実のものとなっている。本記事では、draw.io XMLの仕組みからLLM性能比較、図表タイプ別の実装ガイド、プロンプトエンジニアリング、実務運用のベストプラクティスまでを網羅的に解説する。これにより、図表生成時間を90%削減し、IaC連携で自動同期を実現する技術を習得できる。

## 2. draw.io XMLの仕組み - mxGraphの基礎知識

### 2.1 XML階層構造の全体像

draw.ioの図表は以下の階層構造で定義される[2]：

```
mxfile (ルート要素)
└─ diagram (個別の図を定義、複数可)
   └─ mxGraphModel (描画設定を管理)
      └─ root (mxCell要素のコンテナ)
         ├─ mxCell id="0" (予約セル、親なし)
         ├─ mxCell id="1" parent="0" (デフォルトレイヤー)
         ├─ mxCell id="2" vertex="1" parent="1" (図形要素)
         └─ mxCell id="3" edge="1" parent="1" (接続線)
```

各要素の役割は以下の通りである：

| 要素 | 必須属性 | 役割 |
|------|----------|------|
| `<mxfile>` | host, modified, agent | ドキュメント全体のメタ情報 |
| `<diagram>` | id, name | 個別ページの定義 |
| `<mxGraphModel>` | dx, dy, grid, gridSize | キャンバス設定（グリッド、ズーム等） |
| `<root>` | なし | mxCellのコンテナ |
| `<mxCell>` | id, parent | 図形（vertex）または接続線（edge） |

**重要な注意点**：`id="0"`と`id="1"`は予約済みであり、これらを欠落させると図が表示されない[2]。LLMにXML生成を依頼する際は、必ずこれらの要素を含むようプロンプトで指示する必要がある。

### 2.2 座標系とレイアウト原則

mxGeometry属性は図形の位置とサイズを定義する[6]。vertexとedgeで挙動が異なるため、正確な理解が必要である：

| 要素タイプ | relative | x | y | width | height |
|-----------|----------|---|---|-------|--------|
| vertex（図形） | false | 絶対X座標（px） | 絶対Y座標（px） | 幅（px） | 高さ（px） |
| edge（接続線） | true | -1～1（中心からの距離） | 垂直距離（px） | ラベル幅 | ラベル高さ |

vertexは親セルの原点からの絶対座標で配置される。一方、edgeは接続点の中心からの相対座標（x=0が中心、x=1が右端、x=-1が左端）で表現される。この違いを理解していないと、LLMが生成したXMLで座標がずれる原因となる。

**推奨レイアウトパラメータ**[7]：

| パラメータ | 推奨値 | 理由 |
|----------|--------|------|
| 垂直方向間隔 | 100px | ノード間の読みやすさ確保 |
| 水平方向間隔 | 200px | グループ間の明確な分離 |
| ページサイズ | 1169x827 | A4横向き相当、印刷・共有に最適 |
| 中央配置基準X | 250-350 | 標準ページ内での視認性 |
| フォントサイズ | 11px | draw.ioデフォルト、可読性良好 |

これらのパラメータをプロンプトに含めることで、LLMが生成する図表の視認性が大幅に向上する。

### 2.3 スタイル属性の完全リファレンス

draw.ioのスタイル属性はセミコロン区切りの文字列で定義される[8]。主要属性は以下の通りである：

| 属性名 | 型 | 値の例 | 説明 |
|--------|---|--------|------|
| fillColor | string | #dae8fc, swimlane | 塗りつぶし色 |
| strokeColor | string | #6c8ebf, red | 線の色 |
| strokeWidth | float | 1.0, 2.5 | 線の太さ |
| fontSize | int | 11, 14 | フォントサイズ |
| fontColor | string | #000000, white | テキスト色 |
| gradientColor | string | #7ea6e0 | グラデーション終点色 |

スタイル文字列の記法例：

```
rounded;strokeColor=red;fillColor=green;fontSize=12
```

色分け戦略を一貫して適用することで、要素タイプ（サービス、データベース、ネットワーク等）の識別性が向上する。例えば、サービスは`#dae8fc`、データベースは`#d5e8d4`、ネットワークは`#ffe6cc`のように色コードを統一すると、生成された図表の可読性が高まる[7]。

### 2.4 XMLの手動編集とデバッグ

LLMが生成したXMLを微調整したい場合、draw.ioには直接編集機能が用意されている[15]：

1. draw.ioメニューで「Extras > Edit Diagram」を選択
2. テキストエディタで`<mxGraphModel>`タグ内を編集
3. 変更を保存して図表に反映

デフォルトではXMLが標準deflateで圧縮されているため[16]、バージョン管理やデバッグには非圧縮保存が推奨される：

- **非圧縮保存**: File > Properties で「Compressed」チェックボックスを外す
- **XML出力**: File > Export as > XML で`<?xml version="1.0"?>`付きで出力

Gitで差分管理する場合は、非圧縮XMLとして保存することで、変更箇所を明確に追跡できる。

## 3. LLM性能比較 - Claude 3.7が最強である理由

### 3.1 主要LLMの図表生成精度ベンチマーク

2025年時点での主要LLMの図表生成性能を比較すると、Claude 3.7 Sonnetが最も高い精度を示している[3]：

| モデル | AWS構成図精度 | 座標計算安定性 | アイコン認識 | 生成時間（平均） |
|--------|--------------|---------------|-------------|----------------|
| Claude 3.7 Sonnet | ★★★★★ | ★★★★★ | ★★★★★ | 90秒 |
| Claude 3.5 Sonnet | ★★★★☆ | ★★★★☆ | ★★★★☆ | 80秒 |
| GPT-4o | ★★★☆☆ | ★★★☆☆ | ★★☆☆☆ | 120秒 |
| その他 | ★★☆☆☆ | ★★☆☆☆ | ★☆☆☆☆ | - |

実際の検証では、Claude 3.7はTerraformコードから正確なAWS構成図を生成し、VPC、サブネット、EC2、RDS、ロードバランサーの配置と接続が論理的に整合している[3]。一方、GPT-4oはAWSアイコンの認識に課題があり、座標計算でもばらつきが見られた。

### 3.2 Claude 3.7推奨の技術的根拠

Claude 3.7 Sonnetが優れている理由は以下の4点である[4][5]：

1. **mxGraph XMLスキーマの学習精度**: id="0"とid="1"の予約セル、mxGeometry属性の仕様、スタイル文字列の記法を正確に理解している
2. **座標計算ロジックの安定性**: 垂直100px、水平200pxの間隔原則を自動的に適用し、重複や大幅なずれが少ない
3. **アイコンライブラリ認識**: 「AWS 2025アイコンセット」のような年号指定に対応し、最新のアイコン形状を反映できる
4. **生成時間と品質のトレードオフ**: 複雑な図でも2分以内に完成し、段階的生成の必要性が低い

実務では「そのまま客先には出せないだろうけど、メンバー内で共有する分には十分」[19]という評価が妥当であり、LLM生成80% + 手動微調整20%の併用戦略が推奨される。

## 4. 図表タイプ別実装ガイド

### 4.1 AWS/Azureシステム構成図

**プロンプトテンプレート**：

```
draw.ioで使用できるXMLを書いて
以下のTerraformコードで構築されたAWSインフラの構成図を作成してください。
AWS 2025アイコンセットを使用し、水平レイアウトで配置してください。

[Terraformコード]
```

**IaC連携ワークフロー**[18]：

1. AWS CLIでリソース情報を抽出（`aws ec2 describe-instances`, `aws rds describe-db-instances`等）
2. TerraformコードまたはCDKコードをプロンプトに含める
3. Claude 3.7にdraw.io XML形式での構成図生成を依頼
4. draw.ioエディタで微調整（接続線の整列、ラベル位置の調整）

**XMLサンプルコード**（VPC/サブネット/EC2/RDS/LB構成例）：

```xml
<mxfile host="app.diagrams.net">
  <diagram name="AWS構成図" id="aws-architecture">
    <mxGraphModel dx="1422" dy="794" grid="1" gridSize="10" guides="1">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- VPC -->
        <mxCell id="vpc" value="VPC&#xa;10.0.0.0/16" style="rounded=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="600" height="400" as="geometry"/>
        </mxCell>

        <!-- Public Subnet -->
        <mxCell id="public-subnet" value="Public Subnet&#xa;10.0.1.0/24" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="150" y="150" width="200" height="150" as="geometry"/>
        </mxCell>

        <!-- Private Subnet -->
        <mxCell id="private-subnet" value="Private Subnet&#xa;10.0.2.0/24" style="rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="450" y="150" width="200" height="150" as="geometry"/>
        </mxCell>

        <!-- Load Balancer -->
        <mxCell id="alb" value="Application&#xa;Load Balancer" style="rounded=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="200" y="180" width="100" height="60" as="geometry"/>
        </mxCell>

        <!-- EC2 -->
        <mxCell id="ec2" value="EC2&#xa;Instance" style="rounded=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="500" y="180" width="100" height="60" as="geometry"/>
        </mxCell>

        <!-- RDS -->
        <mxCell id="rds" value="RDS&#xa;PostgreSQL" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="500" y="350" width="100" height="60" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="edge1" edge="1" parent="1" source="alb" target="ec2">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge2" edge="1" parent="1" source="ec2" target="rds">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

このXMLをdraw.ioで開くと、VPC内にパブリックサブネットとプライベートサブネットが配置され、ALB→EC2→RDSの接続が可視化される。

### 4.2 フローチャート・業務プロセス図

**プロンプトテンプレート**：

```
draw.ioで使えるXMLを書いて
ECサイトの注文から発送までのフローチャートを作成してください。
開始・処理・判断・終了の各ステップを明示し、垂直レイアウトで配置してください。
```

**XMLサンプルコード**（5ステップのフロー例）：

```xml
<mxfile host="app.diagrams.net">
  <diagram name="フローチャート" id="flowchart">
    <mxGraphModel dx="1422" dy="794" grid="1" gridSize="10" guides="1">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- Start -->
        <mxCell id="start" value="開始" style="ellipse;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="250" y="50" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- Process 1 -->
        <mxCell id="process1" value="注文受付" style="rounded=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="250" y="150" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- Decision -->
        <mxCell id="decision" value="在庫あり?" style="rhombus;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="250" y="250" width="100" height="80" as="geometry"/>
        </mxCell>

        <!-- Process 2 -->
        <mxCell id="process2" value="決済処理" style="rounded=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="250" y="380" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- Process 3 -->
        <mxCell id="process3" value="発送" style="rounded=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="250" y="480" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- End -->
        <mxCell id="end" value="終了" style="ellipse;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="250" y="580" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="edge1" edge="1" parent="1" source="start" target="process1">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge2" edge="1" parent="1" source="process1" target="decision">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge3" value="はい" edge="1" parent="1" source="decision" target="process2">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge4" edge="1" parent="1" source="process2" target="process3">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge5" edge="1" parent="1" source="process3" target="end">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

判断分岐（ダイヤモンド形状）は`style="rhombus"`で定義される。エッジに「はい」「いいえ」のラベルを付与する場合は、`<mxCell>`のvalue属性にテキストを設定する。

### 4.3 スイムレーン図（クロスファンクショナル図）

**プロンプトテンプレート**：

```
draw.ioで使えるXMLを書いて
システム開発のスイムレーン図を作成してください。
レーン: PM、開発、QA、インフラ
フェーズ: 要件定義→設計→実装→テスト→デプロイ
```

スイムレーン図では、プールシェイプ（pool shapes）をコンテナとして使用する[11]。各レーンは自動的に子要素を保持し、Arrange > Insert > Template > Flowchartsからテンプレートを選択することで、基本構造を迅速に作成できる。

**XMLサンプルコード**（3レーン×4フェーズの例）：

```xml
<mxfile host="app.diagrams.net">
  <diagram name="スイムレーン図" id="swimlane">
    <mxGraphModel dx="1422" dy="794" grid="1" gridSize="10" guides="1">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- PM Lane -->
        <mxCell id="pm-lane" value="PM" style="swimlane;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="600" height="100" as="geometry"/>
        </mxCell>
        <mxCell id="pm-req" value="要件定義" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="pm-lane">
          <mxGeometry x="20" y="30" width="100" height="40" as="geometry"/>
        </mxCell>

        <!-- Dev Lane -->
        <mxCell id="dev-lane" value="開発" style="swimlane;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="100" y="200" width="600" height="100" as="geometry"/>
        </mxCell>
        <mxCell id="dev-design" value="設計" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="dev-lane">
          <mxGeometry x="150" y="30" width="100" height="40" as="geometry"/>
        </mxCell>
        <mxCell id="dev-impl" value="実装" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="dev-lane">
          <mxGeometry x="300" y="30" width="100" height="40" as="geometry"/>
        </mxCell>

        <!-- QA Lane -->
        <mxCell id="qa-lane" value="QA" style="swimlane;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="100" y="300" width="600" height="100" as="geometry"/>
        </mxCell>
        <mxCell id="qa-test" value="テスト" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="qa-lane">
          <mxGeometry x="450" y="30" width="100" height="40" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="edge1" edge="1" parent="1" source="pm-req" target="dev-design">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge2" edge="1" parent="1" source="dev-design" target="dev-impl">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge3" edge="1" parent="1" source="dev-impl" target="qa-test">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

スイムレーン図の各要素は`parent`属性でレーンに所属させる。レーン間のフローは通常の`edge`要素で接続する。

### 4.4 組織図・体制図

**プロンプトテンプレート**：

```
draw.ioで使えるXMLを書いて
以下の階層構造の組織図を作成してください。
CEO → CTO, CFO, COO
CTO → VP Engineering, VP Product
VP Engineering → Backend Lead, Frontend Lead, SRE Lead
```

組織図はテキスト/CSVデータから自動生成できる[12]。Arrange > Insert > Layout > Org Chartで自動整列機能を使用すると、階層関係が視覚的に明確になる。

**XMLサンプルコード**（3階層組織図）：

```xml
<mxfile host="app.diagrams.net">
  <diagram name="組織図" id="org-chart">
    <mxGraphModel dx="1422" dy="794" grid="1" gridSize="10" guides="1">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- CEO -->
        <mxCell id="ceo" value="CEO" style="rounded=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="300" y="50" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- CTO -->
        <mxCell id="cto" value="CTO" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="150" y="150" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- CFO -->
        <mxCell id="cfo" value="CFO" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="300" y="150" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- COO -->
        <mxCell id="coo" value="COO" style="rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="450" y="150" width="100" height="50" as="geometry"/>
        </mxCell>

        <!-- VP Engineering -->
        <mxCell id="vp-eng" value="VP Engineering" style="rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="50" y="250" width="120" height="50" as="geometry"/>
        </mxCell>

        <!-- VP Product -->
        <mxCell id="vp-prod" value="VP Product" style="rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11" vertex="1" parent="1">
          <mxGeometry x="200" y="250" width="120" height="50" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="edge1" edge="1" parent="1" source="ceo" target="cto">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge2" edge="1" parent="1" source="ceo" target="cfo">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge3" edge="1" parent="1" source="ceo" target="coo">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge4" edge="1" parent="1" source="cto" target="vp-eng">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge5" edge="1" parent="1" source="cto" target="vp-prod">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

組織図では垂直方向の間隔を100pxで統一し、同階層の要素は水平方向に200px間隔で配置すると視認性が高まる。

### 4.5 ER図・データモデル図

**プロンプトテンプレート**：

```
draw.ioでXMLを書いて
顧客テーブル、商品テーブル、注文テーブルのER図を作成してください。
顧客と注文は1対多、注文と商品は多対多の関係です。
```

ER図ではエンティティ（四角形）とリレーション（接続線）で表現する。カーディナリティ（1:N, N:M）は接続線のラベルで明示する。

**XMLサンプルコード**（3テーブルのER図）：

```xml
<mxfile host="app.diagrams.net">
  <diagram name="ER図" id="er-diagram">
    <mxGraphModel dx="1422" dy="794" grid="1" gridSize="10" guides="1">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- Customer Entity -->
        <mxCell id="customer" value="顧客&#xa;id (PK)&#xa;name&#xa;email" style="rounded=0;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11;align=left" vertex="1" parent="1">
          <mxGeometry x="100" y="150" width="120" height="80" as="geometry"/>
        </mxCell>

        <!-- Order Entity -->
        <mxCell id="order" value="注文&#xa;id (PK)&#xa;customer_id (FK)&#xa;order_date" style="rounded=0;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=11;align=left" vertex="1" parent="1">
          <mxGeometry x="350" y="150" width="150" height="80" as="geometry"/>
        </mxCell>

        <!-- Product Entity -->
        <mxCell id="product" value="商品&#xa;id (PK)&#xa;name&#xa;price" style="rounded=0;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11;align=left" vertex="1" parent="1">
          <mxGeometry x="600" y="150" width="120" height="80" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="edge1" value="1:N" edge="1" parent="1" source="customer" target="order">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="edge2" value="N:M" edge="1" parent="1" source="order" target="product">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

ER図では`align=left`を指定することで、属性リストを左揃えで見やすく表示できる。

## 5. プロンプトエンジニアリング - 高品質生成の技法

### 5.1 失敗防止テンプレート設計原則

LLMにdraw.io XMLを生成させる際、以下の要素を必ず含めるようプロンプトで指示する[14]：

1. **XML宣言とmxfile構造**: `<mxfile host="app.diagrams.net">`で開始
2. **id="0"とid="1"の予約**: `<mxCell id="0"/>`と`<mxCell id="1" parent="0"/>`を明示
3. **全vertex要素へのgeometry定義**: x, y, width, heightを必ず指定
4. **一貫したスタイル適用**: 要素タイプごとに色分けルールを統一

**失敗防止プロンプト例**：

```
draw.ioで使用できるXMLを書いて、以下の要件を満たしてください：
- mxCellのid="0"とid="1"を必ず含める
- すべてのvertex要素にmxGeometry（x, y, width, height）を定義
- 垂直方向の間隔は100px、水平方向の間隔は200pxで配置
- サービスは#dae8fc、データベースは#d5e8d4、ネットワークは#ffe6ccで色分け

[具体的な図の内容]
```

### 5.2 段階的生成アプローチ

複雑な図を一度に生成すると、生成時間が2分を超えて精度が低下するリスクがある[13]。以下の段階的アプローチが推奨される：

1. **単純構造**: 基本的なノードとエッジのみを生成
2. **プロセス重視**: 接続関係を明確にし、フローを視覚化
3. **意思決定重視**: 判断分岐や条件分岐を追加

各段階で生成したXMLをdraw.ioで開き、レイアウトが気に入らない場合はCtrl+Z（Mac: Cmd+Z）でリセットしてから次を適用する[20]。

### 5.3 レイアウト最適化テクニック

レイアウトパラメータを具体的に指定することで、LLMの出力品質が安定する[7]：

| パラメータ | 推奨値 | 理由 |
|----------|--------|------|
| 垂直方向間隔 | 100px | ノード間の読みやすさ確保 |
| 水平方向間隔 | 200px | グループ間の明確な分離 |
| ページサイズ | 1169x827 | A4横向き相当、印刷・共有に最適 |
| 中央配置基準X | 250-350 | 標準ページ内での視認性 |
| フォントサイズ | 11px | draw.ioデフォルト、可読性良好 |

これらの値をプロンプトに含める例：

```
draw.ioでXMLを書いて
ページサイズは1169x827、垂直間隔100px、水平間隔200pxで配置し、
中央配置の基準X座標は300としてください。

[具体的な図の内容]
```

### 5.4 色分けとスタイル統一戦略

要素タイプ別の色コード例[7]：

- **サービス**: `#dae8fc`（淡い青）
- **データベース**: `#d5e8d4`（淡い緑）
- **ネットワーク**: `#ffe6cc`（淡いオレンジ）

グラデーション活用の例：

```
fillColor=#dae8fc;gradientColor=#7ea6e0
```

企業ブランディングに対応する場合は、カスタムカラーパレットを定義し、すべての図表で統一することでドキュメント全体の一貫性が向上する。

## 6. 実務運用のベストプラクティス

### 6.1 IaC連携の自動化ワークフロー

Terraform/CDKのデプロイと同時にdraw.io構成図を自動生成するワークフローは、以下のように構築できる[18]：

**GitHub Actions統合例**：

```yaml
name: Auto-generate draw.io diagram

on:
  push:
    branches:
      - main
    paths:
      - 'terraform/**'

jobs:
  generate-diagram:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Extract AWS resources
        run: |
          aws ec2 describe-instances --output json > instances.json
          aws rds describe-db-instances --output json > rds.json

      - name: Generate draw.io XML via Claude API
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          curl https://api.anthropic.com/v1/messages \
            -H "x-api-key: $ANTHROPIC_API_KEY" \
            -H "anthropic-version: 2023-06-01" \
            -H "content-type: application/json" \
            -d '{
              "model": "claude-3-7-sonnet-20250219",
              "max_tokens": 4096,
              "messages": [{
                "role": "user",
                "content": "draw.ioで使用できるXMLを書いて、以下のTerraformコードからAWS構成図を作成してください。AWS 2025アイコン使用、水平レイアウト。\n\n'$(cat terraform/main.tf)'"
              }]
            }' > diagram.xml

      - name: Commit and push diagram
        run: |
          git add diagram.xml
          git commit -m "Auto-update AWS architecture diagram"
          git push
```

このワークフローにより、Terraformコードが変更されるたびに構成図が自動更新され、「図とコードの乖離」が解消される。

### 6.2 手動編集との併用戦略

実務では「LLM生成80% + 手動微調整20%」の黄金比が推奨される[19]。具体的な判断基準：

- **内部共有なら十分**: チーム内のレビュー、設計討議、ドキュメント作成
- **客先提出は要調整**: プレゼン資料、提案書、公式ドキュメント

draw.ioエディタでの最終チェック項目：

- 接続線の整列（Arrange > Align > Centerで中央揃え）
- ラベル位置の調整（ダブルクリックでテキスト編集モード）
- 色の微調整（右クリック > Edit Style）

### 6.3 チーム共有とテンプレート管理

プロンプトライブラリをGitで管理することで、チーム全体で一貫した図表品質を維持できる。推奨ディレクトリ構成：

```
.
├── prompts/
│   ├── aws-architecture.txt
│   ├── flowchart.txt
│   ├── swimlane.txt
│   └── org-chart.txt
├── templates/
│   ├── aws-base.drawio
│   └── flowchart-base.drawio
└── README.md
```

VSCode拡張機能「Draw.io Integration」を使用すると、VSCode内でdraw.io図表を編集でき、開発フローがシームレスになる。

### 6.4 品質保証とレビュープロセス

生成図の検証項目：

1. **座標整合性**: 重複や大幅なずれがないか
2. **スタイル一貫性**: 色分けルールが守られているか
3. **情報正確性**: ラベル、接続関係がソースコード/要件と一致しているか

draw.ioの自動整列機能を活用：

- **水平/垂直の均等配置**: Arrange > Distribute > Horizontally/Vertically
- **グリッドにスナップ**: View > Snap to Grid

## 7. トラブルシューティング

### 7.1 よくあるエラーと解決策

| エラー | 原因 | 解決策 |
|-------|------|--------|
| 図が表示されない | id="0"/"1"の欠落 | `<mxCell id="0"/>`と`<mxCell id="1" parent="0"/>`を追加 |
| 座標がずれる | relative属性の誤用 | vertexは`relative="false"`、edgeは`relative="true"` |
| スタイルが反映されない | スタイル文字列の構文エラー | `key1=value1;key2=value2`形式を確認 |
| 生成時間が3分超 | プロンプトが過度に複雑 | 図を2-3個に分割して段階的生成 |
| AWSアイコンが認識されない | LLMモデルの限界 | Claude 3.7使用、アイコンセット年を明示（AWS 2025 icons） |

### 7.2 レイアウト崩れの修正手順

1. Extras > Edit DiagramでXMLを開く
2. `<mxGeometry>`要素のx, y値を確認
3. 垂直間隔100px、水平間隔200pxの原則で再配置
4. Arrange > Layout > Horizontalで自動整列を試行

**修正前**：

```xml
<mxCell id="node1" vertex="1" parent="1">
  <mxGeometry x="50" y="50" width="100" height="50" as="geometry"/>
</mxCell>
<mxCell id="node2" vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="100" height="50" as="geometry"/>
</mxCell>
```

**修正後**：

```xml
<mxCell id="node1" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="50" as="geometry"/>
</mxCell>
<mxCell id="node2" vertex="1" parent="1">
  <mxGeometry x="100" y="200" width="100" height="50" as="geometry"/>
</mxCell>
```

### 7.3 パフォーマンス最適化

大規模図でのパフォーマンス改善策：

- **XML圧縮の有効化**: File > Properties > Compressed
- **複数ページへの分割**: 1ページあたり30-50要素を目安に
- **不要なスタイル属性の削減**: デフォルト値（fontSize=11等）は省略可能

## 8. 発展的な活用シナリオ

### 8.1 Claude APIとの自動化統合

REST API経由でのdraw.io図表生成は、以下のPythonコードで実現できる：

```python
import anthropic
import json

def generate_drawio_diagram(terraform_code: str) -> str:
    """
    TerraformコードからClaude 3.7でdraw.io XMLを生成
    """
    client = anthropic.Anthropic(api_key="YOUR_API_KEY")

    prompt = f"""
draw.ioで使用できるXMLを書いて、以下のTerraformコードからAWS構成図を作成してください。
AWS 2025アイコンセット使用、水平レイアウト、垂直間隔100px、水平間隔200px。

{terraform_code}
"""

    message = client.messages.create(
        model="claude-3-7-sonnet-20250219",
        max_tokens=4096,
        messages=[{"role": "user", "content": prompt}]
    )

    return message.content[0].text

# バッチ処理: 複数IaCファイルから一括生成
terraform_files = ["main.tf", "network.tf", "database.tf"]
for tf_file in terraform_files:
    with open(tf_file, "r") as f:
        code = f.read()
    xml = generate_drawio_diagram(code)
    with open(f"{tf_file}.drawio", "w") as f:
        f.write(xml)
```

### 8.2 他ツールとの連携

**PlantUML/Mermaid.jsからの移行パス**：

PlantUMLやMermaid.jsで記述していた図表は、同じ構造をプロンプトとして与えることでdraw.io XMLに変換できる。例えば、PlantUMLのシーケンス図を「draw.ioで使えるXMLを書いて、以下のシーケンス図を作成してください」と指示するだけで移行可能である。

**PowerPoint/Google Slidesへの埋め込み**：

draw.ioは「File > Export as > PNG/JPEG」で画像出力できるため、プレゼン資料への組み込みが容易である。さらに、draw.ioの「Embed mode」を使用すると、PowerPointファイル内に編集可能な状態で埋め込むこともできる。

**Confluenceでのdraw.io図表管理**：

Confluenceはdraw.ioプラグインを公式にサポートしており、ページ内で直接編集できる。LLMで生成したXMLをConfluenceにインポートすることで、ドキュメントと図表の一元管理が実現する。

### 8.3 今後の展望

**Claude 4.0以降での精度向上予測**：

Claude 3.7で既に高精度を達成しているが、次世代モデルでは以下の改善が期待される：

- より複雑な図（50要素以上）での座標計算精度向上
- アイコンライブラリの拡充（Azure 2025、GCP 2025等）
- プロンプト長の制約緩和（10000トークン超の大規模IaCコード対応）

**draw.io APIの進化**：

draw.ioは現在、リアルタイムデータ連携（SQL Connector、CSV/JSON import）を実験的に提供している。将来的には、LLM生成XMLをdraw.io APIに直接POSTし、プレビューURLを即座に取得できる仕組みが実現する可能性がある。

**MCP（Model Context Protocol）によるツール統合**：

MCPは複数のAIツールを統合するためのプロトコルであり、draw.io、Terraform、Claude APIをシームレスに連携させる基盤となる。これにより、IaCコードの変更を検知して自動的に構成図を更新し、Slackに通知する、といった高度な自動化が可能になる。

## 9. まとめ

LLM × draw.io XMLは、単なる「作図の自動化」を超えて「設計の自動化」へのパラダイムシフトをもたらしている。draw.io XMLの階層構造（mxfile→diagram→mxGraphModel→root→mxCell）と座標系を理解し、Claude 3.7 Sonnetの高精度な生成能力を活用することで、システム構成図、フロー図、組織図を90%の時間削減で作成できる。

重要なのは、プロンプトエンジニアリングである。失敗防止テンプレート（id="0"/"1"の予約、geometry定義の必須化）、段階的生成（2分ルール）、レイアウト原則（垂直100px/水平200px）の3点セットを押さえることで、生成品質が飛躍的に向上する。実務では生成80% + 手動調整20%の併用戦略が現実的であり、内部共有には十分、客先提出には微調整という判断基準が有効である。

IaC連携により、Terraform/CDKのデプロイと同時に構成図を自動生成すれば、「図とコードの乖離」という長年の課題が解消される。チーム共有可能なプロンプトライブラリとdraw.io XMLテンプレートを整備することで、組織全体の生産性が向上し、ドキュメント品質が標準化される。2025年時点でClaude 3.7 Sonnet + draw.io + IaCの組み合わせが最適解であり、今後のモデル進化とMCP統合により、さらなる自動化の進展が期待される。

## 参考URL

[1] mxGraph API - mxCell
https://jgraph.github.io/mxgraph/docs/js-api/files/model/mxCell-js.html
mxGraphのセル構造とXML要素の対応を定義。draw.ioの基盤ライブラリの公式仕様。

[2] Zenn - draw.io XML文書作成ガイド (フロー図)
https://zenn.dev/centervil/articles/2025-03-14-drawio-xml-creation-guide
XMLの基本構造、mxCell要素、座標系の詳細解説。LLM生成に最適化された実践的ガイド。

[3] DevelopersIO - 生成AIにdraw.ioのAWS構成図を作図させてみた
https://dev.classmethod.jp/articles/aws-drawio-genai/
Claude 3.5/3.7、GPT等のモデル比較実験。IaCコードからの自動生成手法。

[4] Note - 全ビジネスマンが使えるClaude3.7 sonnet と draw.ioで始める図の作成
https://note.com/japanmarketing/n/n6d73751105cc
基本プロンプト「draw.ioで使えるXMLを書いて」の紹介。初心者向け実践例。

[5] Qiita - Claude 3.7 Sonnetの図解作成に驚き、draw.ioやPPTXで編集してみる
https://qiita.com/teraco/items/8d07eddfbb689ce15060
Claude 3.7の出力品質評価、PPTX変換手法、実装検証レポート。

[6] mxGraph API - mxGeometry
https://jgraph.github.io/mxgraph/docs/js-api/files/model/mxGeometry-js.html
座標系（x, y, width, height）の正確な仕様。vertex/edgeの挙動の違い。

[7] Zenn - DrawIO向けXML生成プロンプトテンプレート集
https://zenn.dev/tetsu_san/articles/6694be7e6db017
レイアウトパラメータ（100px垂直間隔、200px水平間隔）、色分け戦略、段階的生成アプローチ。

[8] mxGraph API - mxConstants
https://jgraph.github.io/mxgraph/docs/js-api/files/util/mxConstants-js.html
STYLE_で始まる全スタイル定数のリファレンス。fillColor, strokeColor等の仕様。

[9] DevelopersIO - AWS構成図作成はdraw.ioが最強だと思う
https://ichigaku-engineer.com/drawio-is-best-tool-making-aws-architecture/
AWS構成図作成のベストプラクティス、アイコンライブラリの活用法。

[10] draw.io公式 - Example diagrams and templates
https://www.drawio.com/example-diagrams
フローチャートを含む公式テンプレート集。XMLファイルのダウンロード可能。

[11] draw.io公式ブログ - Working with Swimlanes in draw.io
https://drawio-app.com/blog/working-with-swimlanes-in-draw-io/
スイムレーン図の作成手順、プールシェイプのコンテナ機能、テンプレート選択。

[12] draw.io公式ブログ - Use org charts to categorise data and show hierarchies
https://www.drawio.com/blog/org-charts
組織図のテキスト/CSV自動生成、階層構造の定義（親 -> 子）、自動レイアウト機能。

[13] DiagrammerGPT（COLM 2024論文）
https://diagrammergpt.github.io/
LLMによるダイアグラム生成の理論的基盤。2段階フレームワーク（プランナー→オーディター）。

[14] Zenn - ADoc設計文書からDraw.io XML自動生成ガイド
https://zenn.dev/tetsu_san/articles/6694be7e6db016
AI活用による高品質フローチャート作成、失敗パターンと対策。

[15] draw.io公式FAQ - Manually edit the XML source of your draw.io diagram
https://www.drawio.com/doc/faq/diagram-source-edit
XML手動編集の公式手順、Extras > Edit Diagramメニュー、mxGraphModelタグ。

[16] draw.io公式FAQ - Export your diagram to an XML file
https://www.drawio.com/doc/faq/export-to-xml
XML圧縮の仕組み（deflate）、非圧縮保存オプション、File > Export as > XML。

[17] Zenn - Claude 3.7 + draw.io APIによる実務活用シナリオ
https://zenn.dev/idev/articles/article-20250313-121805
システム構成図、フローチャート、ER図の実務プロンプトテンプレート集。

[18] Zenn - Claude CodeでAWSの構成図とかを書き出してもらった
https://zenn.dev/chatii/articles/51b29c3e17cf6f
AWS CDK + AWS CLIを使った実装例、生成時間と品質のトレードオフ、課題の記録。

[19] 同上（引用箇所）
https://zenn.dev/chatii/articles/51b29c3e17cf6f
「そのまま客先には出せないだろうけど、メンバー内で共有する分には十分なのでは?」生成図の実用性評価。

[20] draw.io公式ブログ - Automatic Layout in draw.io
https://drawio-app.com/blog/automatic-layout-in-draw-io/
自動レイアウトの適用原則、Ctrl+Zによるリセットの重要性、複数レイアウト適用の落とし穴。

[21] draw.io公式ブログ - 5 tips to optimize your draw.io diagrams
https://drawio-app.com/blog/5-tips-to-optimize-your-draw-io-diagrams/
最適化のベストプラクティス、明瞭性の原則、過度な複雑化/簡略化の回避。
