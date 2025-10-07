---
permalink: /suno-v5-prompt-guide-for-beginners
title: "Suno v5完全プロンプトガイド - 音楽知識ゼロでも意図したフィーリングを再現する方法"
summary: "音楽理論を知らなくてもOK。Suno v5で「こんな気分の曲」を3ステップで生成する実践的プロンプトガイド。感情マップ、メタタグ完全解説、15パターンの実例付き。"
tags:
  - "#suno-v5"
  - "#ai-music"
  - "#prompt-engineering"
  - "#music-generation"
  - "#beginner-guide"
  - "#emotion-mapping"
  - "#metatag"
date: 2025-10-07
author: "AI Music Research"
reading_time: "12-15分"
difficulty: "初級〜中級"
target_audience: "音楽知識のないユーザー"
article_type: "実践ガイド"
---

# Suno v5完全プロンプトガイド - 音楽知識ゼロでも意図したフィーリングを再現する方法

Suno v5は2025年9月リリースのAI音楽生成ツール最新版。「爽やかな朝」「切ない夜」などのフィーリングを言語化するだけで、音楽理論不要で意図した楽曲を生成できる。本記事では、3ステップのプロンプトフレームワーク、感情マップ、メタタグ完全解説、15の実践例を通じて、初心者がゼロから「思い通りの音楽」を作る方法を徹底解説する。

## TL;DR（要約）

- **Suno v5の革新**: ボーカル精密制御、ネガティブプロンプト強化、会話的プロンプト対応で初心者でも直感的に使える[1][2]
- **3ステップフレームワーク**: ジャンル + 感情 + 楽器1-2種で完成。専門用語なしでフィーリングを再現可能[3]
- **感情マップ**: 15パターンのフィーリング→プロンプト変換表で「こんな気分」をそのまま音楽に
- **メタタグ**: [Verse], [Chorus]等で楽曲構造を直感的に制御。音楽理論不要で楽曲の流れを設計[4]
- **初心者向けチェックリスト**: 7つの避けるべきミスと解決策で、よくある失敗を回避[5]

---

## 1. Suno v5とは？音楽知識ゼロでも使える理由

### 1-1. Suno v5の3つの革新的機能

Suno v5は2025年9月にリリースされたAI音楽生成の最新モデルで、従来版（v4.5）から大幅な進化を遂げた。特に音楽知識のないユーザーにとって革新的な点は以下の3つだ[1][2]。

**表1-1: v4.5 vs v5の機能比較**

| 機能 | 従来（v4.5） | v5 | 初心者への影響 |
|------|-------------|-----|----------------|
| **会話的プロンプト** | 専門用語必須 | 「uplifting」等の感情語でOK | 音楽理論不要で直感的 |
| **ボーカル精密制御** | 基本的な歌声 | ビブラート、ブレス感まで指定可 | フィーリング再現の精度向上 |
| **ネガティブプロンプト** | 除外が不安定 | 高精度除外 | 意図しないジャンル混入を防止 |
| **楽器分離** | やや不明瞭 | 明確な楽器分離とハイフィデリティ | 各楽器の音がクリアに聞こえる |
| **処理速度** | 標準 | 10倍高速 | 数秒で楽曲生成完了 |

*出典: [1] Suno公式ヘルプ、[2] WebSearch結果統合*

#### 会話的プロンプト対応

v5では、「upbeat pop with catchy melodies（キャッチーなメロディの明るいポップス）」のような**会話的な表現**で意図を伝えられる。従来版では「Pop, 120 BPM, Major key, Synth lead」のような専門用語が必要だったが、v5ではそれが不要になった[2]。

#### ボーカル精密制御

v5のボーカルエンジンは、プロデューサーがスタジオで歌手に指示を出すように、**詳細なボーカル指示**が可能だ。「breathy（息っぽい）」「smoky（煙がかった）」「gentle vibrato at phrase endings（フレーズ末尾で優しいビブラート）」など、感覚的な表現で歌声を制御できる[2][3]。

#### ネガティブプロンプト強化

v5では、「こういう要素は入れないで」という**除外指示の信頼性が大幅向上**した。「no guitars（ギターなし）」「no vocals（歌声なし）」などの指示が高精度で反映され、意図しない要素の混入を防げる[4]。

### 1-2. 「音楽知識ゼロ」でも使える3つの理由

#### 理由1: ジャンル + 感情 + 楽器の3要素だけ

Sunoは、**最小3つの要素**だけで高品質な楽曲を生成できる。例えば「Pop, uplifting, acoustic guitar（明るいポップス、アコースティックギター）」という指定だけで、音楽理論を知らなくても意図したフィーリングを再現可能だ[3]。

#### 理由2: メタタグで構造指示

[Verse], [Chorus]などの**メタタグ**を使えば、楽曲の構造を直感的に制御できる。「Verse（バース）= 物語部分」「Chorus（コーラス）= サビ」という理解だけで、プロのような楽曲構成を作れる[5]。

#### 理由3: 実例豊富なコミュニティ

Suno AIコミュニティには、**2,150以上のプロンプト要素**が日本語で検索可能な状態で公開されている[6]。自分のフィーリングに近い実例をコピー&ペーストするだけで始められる。

**キーメッセージ**: 「こんな気分の曲が欲しい」という感情を言語化できれば、誰でもプロ品質の楽曲を生成できる。音楽理論、楽器の演奏技術、作曲スキルは一切不要だ。

### 1-3. この記事で学べること

本記事を読むことで、以下のスキルを習得できる：

- ✅ **3ステップで完成するプロンプトの書き方** - ジャンル、感情、楽器を組み合わせる基本フレームワーク
- ✅ **15パターンのフィーリング→プロンプト変換マップ** - 「爽やかな朝」「切ない夜」などの感情を具体的なプロンプトに変換
- ✅ **メタタグを使った楽曲構造の制御方法** - [Verse], [Chorus]等で楽曲の流れを設計
- ✅ **初心者が陥りがちな7つのミスと解決策** - 「意図と違う曲ができる」問題を事前に回避
- ✅ **トラブルシューティング** - うまくいかないときの対処法

**所要時間**: 本記事を読んで最初の1曲を作るまで、約30分。

---

## 2. 基本中の基本 - 3ステップフレームワーク

音楽知識ゼロから始めるための最小構成は、**ジャンル + 感情 + 楽器**の3ステップだ。専門用語なしで、フィーリングを音楽に変換できる[3][7]。

### 2-1. Step 1: ジャンルを選ぶ（音楽理論不要）

**Q: ジャンルって何？**
→ 音楽のスタイルのこと。「ポップス」「ロック」「ジャズ」など。

#### 初心者向けジャンル選びガイド

| フィーリング | 推奨ジャンル | 理由 |
|--------------|--------------|------|
| **明るく元気** | Pop | キャッチーで親しみやすい |
| **かっこいい** | Rock | エネルギッシュでパワフル |
| **落ち着いた** | Jazz, Ballad | 穏やかでリラックス |
| **切ない** | Ballad, Indie Pop | 感情表現が豊か |
| **リズミカル** | Hip-Hop, EDM | ビート重視 |
| **大人っぽい** | Jazz, Blues | 洗練された雰囲気 |
| **自然な感じ** | Folk, Country | アコースティックで温かい |

**重要**: Suno v5では**1-2ジャンルまで**が推奨。3種以上のジャンルを指定すると、AIが混乱して意図しないミックスになる可能性が高い[2][8]。

#### ジャンルの組み合わせ例

| 組み合わせ | 結果の雰囲気 |
|-----------|-------------|
| **Pop Rock** | 明るくエネルギッシュ |
| **Jazz Ballad** | 大人っぽく感情的 |
| **Indie Folk** | 自然で温かい |
| **Trap Metal** | 激しく攻撃的 |

### 2-2. Step 2: 感情・ムードを言語化する

**Q: どんな言葉が使える？**

感情を表す英単語（日本語でも可）を1つ選ぶ。複数の感情を指定すると矛盾が生じるため、**1つに絞る**のが推奨[2][7]。

#### ポジティブ系感情ワード

| 英語 | 日本語 | 使用シーン |
|------|--------|-----------|
| **uplifting** | 高揚感、前向き | 朝、新しいスタート |
| **joyful** | 喜びに満ちた | お祝い、ハッピーな瞬間 |
| **energetic** | エネルギッシュ | スポーツ、ワークアウト |
| **hopeful** | 希望に満ちた | 挑戦、冒険 |
| **triumphant** | 勝利感、達成感 | 目標達成、成功 |

#### ネガティブ系感情ワード

| 英語 | 日本語 | 使用シーン |
|------|--------|-----------|
| **melancholic** | 憂鬱、哀愁 | 別れ、失恋 |
| **somber** | 陰鬱な | 雨の日、沈んだ気分 |
| **wistful** | 物思いにふけった | 過去を振り返る |
| **tense** | 緊張感のある | 不安、サスペンス |

#### ニュートラル系感情ワード

| 英語 | 日本語 | 使用シーン |
|------|--------|-----------|
| **dreamy** | 夢見心地 | リラックス、瞑想 |
| **serene** | 穏やかな | カフェ、作業用 |
| **mysterious** | 神秘的な | ファンタジー、ミステリー |
| **intense** | 激しい、強烈な | ドラマチックな展開 |

**推奨**: フィーリングを**形容詞1つ**で表現するのが最も効果的。「uplifting and energetic」のように複数指定すると、どちらを優先すべきか不明確になる[7]。

### 2-3. Step 3: 楽器を1-2種選ぶ

**Q: 楽器の知識がないんだけど…**

楽器の正式名称や演奏方法を知らなくても大丈夫。**音の特徴**から選べばOK。

#### 初心者向け楽器選びガイド

| 楽器 | 音の特徴 | おすすめシーン |
|------|----------|----------------|
| **Acoustic guitar** | 温かく柔らかい | 朝、リラックス、自然な雰囲気 |
| **Piano** | クリアで感情的 | 切ないシーン、バラード |
| **Saxophone** | 滑らかでジャズっぽい | 大人っぽい雰囲気、カフェ |
| **Electric guitar** | パワフルでかっこいい | エネルギッシュな曲、ロック |
| **Strings（弦楽器）** | 壮大で映画的 | ドラマチックな展開、感動 |
| **808 bass** | ズンズンと響く低音 | Hip-Hop、ダンス、クラブ |
| **Synths（シンセサイザー）** | 電子的で未来的 | EDM、ポップス |
| **Drums** | リズム重視 | エネルギッシュ、ダンス |

**重要**: 楽器は**1-2種まで**。3-4種以上指定すると、音が混ざって各楽器の特徴が不明瞭になる[2][8]。

#### 楽器の組み合わせ例

| 組み合わせ | 結果の雰囲気 |
|-----------|-------------|
| **Acoustic guitar + Piano** | 温かく感情的 |
| **Electric guitar + Drums** | パワフルでエネルギッシュ |
| **Saxophone + Piano** | ジャズ風で大人っぽい |
| **808 bass + Synths** | クラブ向けEDM |

### 2-4. 3ステップを組み合わせる - 実例

#### 例1: 爽やかな朝

```
Pop, uplifting, acoustic guitar
```

**期待される結果**: 明るくポジティブ、朝のルーティンに最適なポップス。アコースティックギターの柔らかい音色が心地よい目覚めを演出。

---

#### 例2: 切ない夜

```
Ballad, melancholic, piano
```

**期待される結果**: 静かで感情的なバラード。ピアノの繊細な音色が切ない気持ちを表現。失恋ソングや別れのシーンに最適。

---

#### 例3: エネルギッシュ

```
Rock, energetic, electric guitar
```

**期待される結果**: パワフルでエネルギッシュなロック。エレキギターの力強い音がモチベーションを高める。ワークアウトやスポーツシーンに。

---

#### 例4: リラックス

```
Jazz, serene, saxophone
```

**期待される結果**: 穏やかで落ち着いたジャズ。サックスの滑らかな音色がリラックスタイムに最適。カフェや読書のBGMに。

---

**図2-1: 3ステップフレームワーク図解**

```
[ジャンル] → Pop, Rock, Jazz, Ballad, Hip-Hop, EDM...
     ↓
[感情] → uplifting, melancholic, energetic, serene...
     ↓
[楽器] → acoustic guitar, piano, saxophone, electric guitar...
     ↓
完成！
```

**表2-1: フィーリング別プロンプト早見表**

| フィーリング | プロンプト | 期待される結果 |
|--------------|-----------|----------------|
| 爽やかな朝 | `Pop, uplifting, acoustic guitar` | 明るくポジティブ、朝のルーティンに最適 |
| 切ない夜 | `Ballad, melancholic, piano` | 静かで感情的、失恋ソング向け |
| エネルギー爆発 | `Rock, energetic, electric guitar` | パワフル、ワークアウト向け |
| リラックス | `Jazz, serene, saxophone` | 穏やか、カフェ向け |
| ロマンティック | `Jazz Ballad, romantic, piano, saxophone` | 大人の恋愛、ディナー向け |
| 集中作業 | `Ambient, minimal, soft pads, no vocals` | 控えめ、作業用BGM |
| 夏のビーチ | `Tropical House, cheerful, steel drums` | 南国感、夏のパーティー向け |
| 深夜の孤独 | `Lo-fi Hip Hop, introspective, piano, 70 BPM` | 内省的、作業用 |
| 神秘的な森 | `Celtic, mysterious, flute, harp` | 幻想的、RPG向け |
| ワクワクする冒険 | `Folk, hopeful, acoustic guitar, 120 BPM` | 前向き、ロードトリップ向け |

---

## 3. 感情マップ - フィーリングをプロンプトに変換する

「こんな気分の曲が欲しい」というフィーリングを、具体的なプロンプトに変換する方法を15パターンで示す。各パターンには、**フィーリング（日本語）**、**プロンプト（英語）**、**期待される結果**を記載している[3][7][9]。

### 3-1. ポジティブ感情系（5パターン）

#### パターン1: 爽やかな朝

**【フィーリング】**: 目覚めスッキリ、新しい一日が始まる感じ。窓を開けて朝日を浴びるような清々しさ。

**【プロンプト】**:
```
Indie Pop, uplifting, acoustic guitar, 115 BPM
```

**【期待される結果】**:
- 明るくポジティブな雰囲気
- アコースティックギターの柔らかい音色
- 朝のルーティン（コーヒーを飲む、ジョギング等）に最適
- 軽快なテンポで心地よい目覚めを演出

**【応用】**: ボーカルを追加したい場合は「bright female vocal（明るい女性ボーカル）」を追加。

---

#### パターン2: ワクワクする冒険

**【フィーリング】**: 旅に出るような期待感。地図を広げて新しい場所へ向かうワクワク感。

**【プロンプト】**:
```
Folk, hopeful, acoustic guitar, light percussion, 120 BPM
```

**【期待される結果】**:
- 前向きで明るい雰囲気
- フォーク調の自然な音色
- ロードトリップ、ドライブのBGMに最適
- 軽快なパーカッションが冒険心を刺激

**【応用】**: より壮大にしたい場合は「strings（弦楽器）」を追加。

---

#### パターン3: 勝利の瞬間

**【フィーリング】**: 達成感、やったぞ！という高揚感。目標を達成した瞬間の爆発的な喜び。

**【プロンプト】**:
```
Rock Anthem, triumphant, electric guitar, drums, 130 BPM
```

**【期待される結果】**:
- 力強く壮大な雰囲気
- エレキギターとドラムの重厚なサウンド
- スポーツの勝利シーン、表彰式に最適
- 高揚感と達成感を最大限に表現

**【応用】**: さらに壮大にしたい場合は「orchestra（オーケストラ）」を追加。

---

#### パターン4: 恋のときめき

**【フィーリング】**: ドキドキ、幸せな恋愛感情。好きな人を思い浮かべるときの心の弾み。

**【プロンプト】**:
```
Pop, joyful, upbeat, piano, light synths, 118 BPM
```

**【期待される結果】**:
- キュートで弾むような雰囲気
- ピアノとシンセの軽やかなサウンド
- 恋愛映画のオープニング、デートシーンに最適
- 幸せな恋愛感情をポップに表現

**【応用】**: ボーカルを追加したい場合は「bright, cheerful vocal（明るく楽しいボーカル）」を追加。

---

#### パターン5: 夏のビーチ

**【フィーリング】**: 開放感、リゾート気分。ビーチでのんびり過ごす幸せな時間。

**【プロンプト】**:
```
Tropical House, cheerful, steel drums, acoustic guitar, 110 BPM
```

**【期待される結果】**:
- 南国感あふれる明るい雰囲気
- スティールドラムの独特な音色
- 夏のパーティー、ビーチイベントに最適
- リゾート気分を自宅で再現

**【応用】**: よりダンサブルにしたい場合は「EDM beats（EDMビート）」を追加。

---

### 3-2. ネガティブ感情系（5パターン）

#### パターン6: 切ない別れ

**【フィーリング】**: 悲しいけど受け入れる、大人の別れ。愛した人との別れを静かに受け止める感情。

**【プロンプト】**:
```
Ballad, melancholic, piano, strings, slow (80 BPM)
```

**【期待される結果】**:
- 静かで感情的な雰囲気
- ピアノと弦楽器の繊細なサウンド
- 失恋ソング、映画のエンディングに最適
- 悲しみを静かに表現

**【応用】**: ボーカルを追加したい場合は「breathy female vocal（息っぽい女性ボーカル）」を追加。

---

#### パターン7: 深夜の孤独

**【フィーリング】**: 一人で考え事、静かな夜。深夜に一人で過ごす内省的な時間。

**【プロンプト】**:
```
Lo-fi Hip Hop, introspective, piano, soft 808 bass, 70 BPM, instrumental only
```

**【期待される結果】**:
- 内省的で静かな雰囲気
- Lo-fi特有のノイズ感と温かみ
- 作業用BGM、深夜の読書に最適
- ボーカルなしでリラックス

**【応用】**: よりジャジーにしたい場合は「smooth jazz chords（滑らかなジャズコード）」を追加。

---

#### パターン8: 雨の日の憂鬱

**【フィーリング】**: どんよりした気分、モヤモヤ。雨音を聞きながら沈んだ気分で過ごす。

**【プロンプト】**:
```
Indie Folk, somber, acoustic guitar, soft strings, 75 BPM
```

**【期待される結果】**:
- 静かで陰鬱な雰囲気
- アコースティックギターの優しい音色
- 雨音と相性良し、室内で静かに過ごす時間に最適
- 憂鬱な気分を音楽で表現

**【応用】**: より重厚にしたい場合は「cello（チェロ）」を追加。

---

#### パターン9: 喪失感

**【フィーリング】**: 何かを失った悲しみ。大切なものを失った時の深い悲しみ。

**【プロンプト】**:
```
Orchestral Ballad, wistful, piano, strings, cello, slow
```

**【期待される結果】**:
- 壮大で感情的な雰囲気
- オーケストラの重厚なサウンド
- 映画のエンディング、追悼シーンに最適
- 深い悲しみを壮大に表現

**【応用】**: ボーカルを追加したい場合は「emotional male vocal（感情的な男性ボーカル）」を追加。

---

#### パターン10: 不安な夜

**【フィーリング】**: 落ち着かない、緊張感。夜中に何かが起こりそうな不安。

**【プロンプト】**:
```
Ambient, tense, dark synths, minimal percussion, 85 BPM
```

**【期待される結果】**:
- 神秘的で緊張感のある雰囲気
- ダークなシンセサイザーの音色
- ホラー、スリラー映画のBGMに最適
- 不安感を音楽で表現

**【応用】**: より不気味にしたい場合は「dissonant chords（不協和音）」を追加。

---

### 3-3. ニュートラル/その他（5パターン）

#### パターン11: リラックスタイム

**【フィーリング】**: 力を抜いてゆっくり。カフェでコーヒーを飲みながらのんびり過ごす時間。

**【プロンプト】**:
```
Jazz, serene, smooth saxophone, soft piano, 90 BPM
```

**【期待される結果】**:
- 穏やかで落ち着いた雰囲気
- サックスとピアノの滑らかなサウンド
- カフェ、読書、リラックスタイムに最適
- 心地よいジャズでストレス解消

**【応用】**: より本格的にしたい場合は「double bass（ダブルベース）」を追加。

---

#### パターン12: 集中作業

**【フィーリング】**: 邪魔されずに集中したい。仕事や勉強に没頭する時間。

**【プロンプト】**:
```
Ambient Electronic, minimal, soft pads, no vocals, 100 BPM
```

**【期待される結果】**:
- 控えめで邪魔しない雰囲気
- 電子音の柔らかいサウンド
- 作業用BGM、勉強に最適
- ボーカルなしで集中力を維持

**【応用】**: よりリズミカルにしたい場合は「gentle beats（優しいビート）」を追加。

---

#### パターン13: 神秘的な森

**【フィーリング】**: ファンタジー、幻想的。異世界の森を探検するような神秘的な感覚。

**【プロンプト】**:
```
Celtic, mysterious, flute, harp, strings, 95 BPM
```

**【期待される結果】**:
- 幻想的で神秘的な雰囲気
- ケルト音楽特有の音色
- RPGゲーム、ファンタジー映画のBGMに最適
- 異世界感を音楽で表現

**【応用】**: より壮大にしたい場合は「choir（合唱）」を追加。

---

#### パターン14: エネルギー爆発

**【フィーリング】**: 激しく動きたい、アドレナリン全開。ジムでのワークアウトやランニングに。

**【プロンプト】**:
```
Trap Metal, intense, distorted guitar, 808 bass, aggressive drums, ~145 BPM
```

**【期待される結果】**:
- 激しく攻撃的な雰囲気
- ディストーションギターの重低音
- ワークアウト、激しいスポーツに最適
- アドレナリンを最大限に引き出す

**【応用】**: ボーカルを追加したい場合は「raspy male vocal, aggressive delivery（かすれた男性ボーカル、攻撃的な歌い方）」を追加。

---

#### パターン15: ロマンティックな夜

**【フィーリング】**: 大人の恋愛、落ち着いたロマンス。ディナーデートやロマンティックな夜に。

**【プロンプト】**:
```
Jazz Ballad, romantic, smooth saxophone, warm Rhodes piano, 85 BPM
```

**【期待される結果】**:
- ロマンティックで洗練された雰囲気
- サックスとローズピアノの温かいサウンド
- ディナー、ロマンティックなシーンに最適
- 大人の恋愛感情を上品に表現

**【応用】**: ボーカルを追加したい場合は「smoky female vocal（煙がかった女性ボーカル）」を追加。

---

**図3-1: 感情マップ（15パターンのビジュアルマップ）**

```
[ポジティブ感情]
├─ 爽やかな朝（Indie Pop, uplifting, acoustic guitar）
├─ ワクワクする冒険（Folk, hopeful, acoustic guitar）
├─ 勝利の瞬間（Rock Anthem, triumphant, electric guitar）
├─ 恋のときめき（Pop, joyful, piano, synths）
└─ 夏のビーチ（Tropical House, cheerful, steel drums）

[ネガティブ感情]
├─ 切ない別れ（Ballad, melancholic, piano, strings）
├─ 深夜の孤独（Lo-fi Hip Hop, introspective, piano）
├─ 雨の日の憂鬱（Indie Folk, somber, acoustic guitar）
├─ 喪失感（Orchestral Ballad, wistful, orchestra）
└─ 不安な夜（Ambient, tense, dark synths）

[ニュートラル/その他]
├─ リラックスタイム（Jazz, serene, saxophone, piano）
├─ 集中作業（Ambient Electronic, minimal, no vocals）
├─ 神秘的な森（Celtic, mysterious, flute, harp）
├─ エネルギー爆発（Trap Metal, intense, distorted guitar）
└─ ロマンティックな夜（Jazz Ballad, romantic, saxophone）
```

---

## 4. メタタグ完全ガイド - 楽曲構造を制御する

メタタグを使えば、音楽理論を知らなくても楽曲の構造を直感的に制御できる。[Verse], [Chorus]などの指示を歌詞欄に記述するだけで、プロのような楽曲構成を作れる[4][5][10]。

### 4-1. メタタグとは？（超初心者向け）

**Q: メタタグって何？**

→ Sunoへの「指示書」のようなもの。`[タグ名]`の形式で歌詞欄に記述し、楽曲の構造を指定する。

**例**:
```
[Verse 1]
歌詞の内容...

[Chorus]
歌詞の内容...
```

#### メタタグの役割

| 役割 | 説明 | 効果 |
|------|------|------|
| **構造の明示** | どこがバース、どこがコーラスかを指示 | AIが楽曲の流れを正しく理解 |
| **セクション間の変化** | 各セクションで音楽的な変化を生成 | バースは静か、コーラスは盛り上がる等 |
| **繰り返しの制御** | コーラスを複数回繰り返す等 | 印象的な部分を強調 |

### 4-2. 基本構造タグ7種類

**表4-1: 基本メタタグ一覧**

| タグ | 意味 | 使うタイミング | 省略可能？ | 役割 |
|------|------|----------------|-----------|------|
| `[Intro]` | イントロ | 楽曲の始まり | ✓ | 楽曲への導入、雰囲気作り |
| `[Verse]` | バース | 物語を進める部分 | × | 歌詞のメインストーリー |
| `[Pre-Chorus]` | プレコーラス | コーラスへの橋渡し | ✓ | 期待感を高める |
| `[Chorus]` | コーラス | 一番印象的な部分（サビ） | × | 楽曲の核心、最も印象的 |
| `[Bridge]` | ブリッジ | 変化をつける部分 | ✓ | 単調さを避ける、転調等 |
| `[Outro]` | アウトロ | エンディング | ✓ | 楽曲の締めくくり |
| `[Break]` | ブレイク | 演奏の中断や変化 | ✓ | リズムの変化、ソロ等 |

*出典: [4] Suno Wiki, [5] 複数ソース統合*

#### 各タグの詳細説明

**[Intro]（イントロ）**
- **役割**: 楽曲の導入部。リスナーを楽曲の世界に引き込む。
- **典型的な内容**: 楽器だけの演奏（`(instrumental, 8 bars)`等）
- **省略可能**: Yes

**[Verse]（バース）**
- **役割**: 歌詞のストーリーを進める部分。通常2-3回繰り返される。
- **典型的な内容**: 物語の展開、状況説明
- **省略可能**: No（楽曲の基本要素）

**[Pre-Chorus]（プレコーラス）**
- **役割**: コーラスへの橋渡し。期待感を高める。
- **典型的な内容**: コーラスへの助走、テンションの上昇
- **省略可能**: Yes

**[Chorus]（コーラス/サビ）**
- **役割**: 楽曲の核心。最も印象的で繰り返される部分。
- **典型的な内容**: 楽曲のメインメッセージ、キャッチーなメロディ
- **省略可能**: No（楽曲の最重要要素）

**[Bridge]（ブリッジ）**
- **役割**: 楽曲に変化をつける。転調やリズムの変化等。
- **典型的な内容**: 内省的な部分、新しい視点
- **省略可能**: Yes

**[Outro]（アウトロ）**
- **役割**: 楽曲の締めくくり。余韻を残す。
- **典型的な内容**: フェードアウト（`(fade out)`）、繰り返し等
- **省略可能**: Yes

**[Break]（ブレイク）**
- **役割**: 演奏の中断や変化。ソロ演奏等。
- **典型的な内容**: `(saxophone solo, 8 bars)`等
- **省略可能**: Yes

### 4-3. 実例で学ぶメタタグの使い方

#### 実例1: シンプルな構成（初心者向け）

```
[Verse 1]
Walking down the empty street
Looking for a place to be

[Chorus]
We are alive, we are free
Dancing in the melody

[Verse 2]
Shadows dancing in the night
Everything will be alright

[Chorus]
We are alive, we are free
Dancing in the melody
```

**構成の解説**:
- **最小限の構成**: Verse（2回）+ Chorus（2回）
- **繰り返し**: コーラスを2回繰り返すことで印象付け
- **省略**: Intro, Bridge, Outroは省略

**期待される結果**: シンプルで覚えやすい楽曲。初心者におすすめの構成。

---

#### 実例2: 標準的な構成（中級者向け）

```
[Intro]
(instrumental, 8 bars)

[Verse 1]
Sun is rising, new day ahead
Feeling grateful for what I have

[Pre-Chorus]
The world is calling my name
Nothing will ever be the same

[Chorus]
It's a beautiful morning
Everything feels right
I'm ready for the day
Bring on the light

[Verse 2]
Coffee brewing, birds are singing
This is the life I'm living

[Pre-Chorus]
The world is calling my name
Nothing will ever be the same

[Chorus]
It's a beautiful morning
Everything feels right
I'm ready for the day
Bring on the light

[Outro]
(fade out with humming)
```

**構成の解説**:
- **完全な構成**: Intro → Verse → Pre-Chorus → Chorus → Verse → Pre-Chorus → Chorus → Outro
- **イントロ**: 楽器だけで導入
- **プレコーラス**: コーラスへの期待感を高める
- **アウトロ**: ハミングでフェードアウト

**期待される結果**: プロのような完成度の高い楽曲。

---

#### 実例3: 高度な構成（感情アーク付き）

```
[Intro]
(piano only, soft, 8 bars)

[Verse 1: Sad mood, piano only]
Lost and alone in the rain
Can't find my way back again

[Pre-Chorus: Hope building, add strings]
But I see a light ahead
Hear the words you said

[Chorus: Triumphant, full band]
We rise above the storm!
Together we are strong!
Nothing can bring us down!
We'll stand our ground!

[Break: Guitar solo, 8 bars]
(distorted electric guitar solo)

[Bridge: Reflective, acoustic]
Looking back at where we've been
All the places we have seen
We've grown stronger through the pain
Dancing in the falling rain

[Chorus: Epic finale, orchestra]
We rise above the storm!
Together we are strong!
Nothing can bring us down!
We'll stand our ground!

[Outro]
(fade out with choir)
```

**構成の解説**:
- **感情アーク**: Sad（悲しい）→ Hopeful（希望）→ Triumphant（勝利）→ Reflective（内省）→ Epic（壮大）
- **メタタグ内の指示**: `[Verse 1: Sad mood, piano only]`のように、メタタグ内に追加指示を記述
- **ブレイク**: ギターソロで変化をつける
- **クライマックス**: 最後のコーラスでオーケストラを追加し、壮大なフィナーレ

**期待される結果**: 感情の変化が明確で、ドラマチックな楽曲。映画のテーマソング級。

---

### 4-4. 高度なメタタグ（オプション）

基本の構造タグに加えて、より詳細な制御が可能な高度なメタタグも存在する[4][10]。

#### ムード・エネルギー制御

```
[Mood: Uplifting]
[Energy: High]
```

**使用例**:
```
[Verse 1: Mood: Melancholic, Energy: Low]
歌詞...

[Chorus: Mood: Triumphant, Energy: High]
歌詞...
```

#### 楽器指定

```
[Instrument: Warm Rhodes]
[Instrument: Strings (Legato)]
```

**使用例**:
```
[Bridge: Instrument: Saxophone solo, 8 bars]
(no lyrics, saxophone solo)
```

#### ボーカルスタイル

```
[Vocal Style: Whisper]
[Vocal Effect: Reverb]
```

**使用例**:
```
[Verse 1: Vocal Style: Breathy, soft]
歌詞...

[Chorus: Vocal Style: Powerful, belt]
歌詞...
```

#### サウンドエフェクト

```
[Bell dings]
[Birds chirping]
[Cheering]
```

**使用例**:
```
[Intro]
[Birds chirping, 4 bars]
(instrumental with nature sounds)
```

**重要**: メタタグは**最初の20-30語**と**セクション変更時**に最も効果的。短く（1-3語）保つのが推奨[4][10]。長すぎるメタタグは無視される可能性がある。

---

**図4-1: 楽曲構造の図解**

```
[Intro] → 導入（8-16小節）
   ↓
[Verse 1] → ストーリー開始
   ↓
[Pre-Chorus] → 期待感を高める（オプション）
   ↓
[Chorus] → サビ（楽曲の核心）
   ↓
[Verse 2] → ストーリー展開
   ↓
[Pre-Chorus] → 期待感を高める（オプション）
   ↓
[Chorus] → サビ（繰り返し）
   ↓
[Bridge] → 変化（転調、新しい視点）（オプション）
   ↓
[Chorus] → サビ（クライマックス）
   ↓
[Outro] → 締めくくり（フェードアウト等）
```

---

## 5. ボーカルとテンポの指定（中級者向け）

より精密なフィーリング再現のために、ボーカルスタイルとテンポ（BPM）の指定方法を解説する[2][3][11]。

### 5-1. ボーカルスタイルの指定（v5の新機能）

**Q: 歌声の雰囲気も指定できる？**

→ Suno v5では、プロデューサーがスタジオで歌手に指示を出すように、詳細なボーカル指示が可能だ[2][3]。

#### 音色（Timbre）の指定

**表5-1: ボーカル音色一覧**

| 指定語 | 音の特徴 | おすすめシーン | 具体例 |
|--------|----------|----------------|--------|
| **breathy** | 息っぽい | 切ない、優しい | バラード、ラブソング |
| **smoky** | 煙がかった | ダーク、セクシー | ジャズ、ブルース |
| **bright** | 明るい | ポップ、元気 | アップテンポなポップス |
| **warm** | 温かい | リラックス、優しい | カフェミュージック |
| **raspy** | かすれた | ロック、力強い | ロック、メタル |
| **airy** | 軽やか、空気感 | 幻想的 | ドリームポップ、エレクトロニカ |
| **nasal** | 鼻にかかった | 個性的 | フォーク、インディー |

#### パフォーマンスキューの指定

| 指定語 | 意味 | 効果 |
|--------|------|------|
| **legato** | 滑らかに（音を繋げる） | 流れるような歌い方 |
| **staccato** | 短く切る | リズミカルで切れのある歌い方 |
| **gentle vibrato at phrase endings** | フレーズ末尾で優しいビブラート | 感情的な余韻 |
| **tight staccato in pre-chorus** | プレコーラスで短く切る | 緊張感、期待感 |
| **medium-speed vibrato** | 中速のビブラート | 自然な表現力 |

#### 具体例

**例1: 切ないバラード**

```
Style: Pop Ballad
Vocal: Female, breathy, gentle vibrato at phrase endings
Mood: Melancholic
Instruments: Piano, strings
```

**期待される結果**: 息っぽい女性ボーカルが切なさを表現。フレーズ末尾のビブラートで余韻を残す。

---

**例2: 力強いロック**

```
Style: Rock
Vocal: Male, raspy, powerful delivery
Mood: Energetic
Instruments: Electric guitar, drums
```

**期待される結果**: かすれた男性ボーカルが力強さを表現。ロックの激しさを最大限に引き出す。

---

**例3: 大人のジャズ**

```
Style: Jazz
Vocal: Female, smoky, legato phrasing
Mood: Romantic
Instruments: Saxophone, warm Rhodes piano
```

**期待される結果**: 煙がかった女性ボーカルが大人の色気を表現。滑らかなフレージングでジャジーな雰囲気。

---

#### ボーカルスタイル×感情の組み合わせマトリックス

**表5-2: ボーカルスタイル×感情マトリックス**

| 感情 | 推奨ボーカルスタイル | プロンプト例 |
|------|----------------------|--------------|
| **切ない** | breathy, soft | `breathy female vocal, soft delivery` |
| **力強い** | confident, bright | `confident male vocal, bright tone` |
| **幻想的** | airy, ethereal | `airy vocal, ethereal tones` |
| **ダーク** | smoky, raspy | `smoky vocal, raspy delivery` |
| **ロマンティック** | warm, smooth | `warm female vocal, smooth legato` |
| **激しい** | aggressive, raspy | `raspy male vocal, aggressive delivery` |

### 5-2. テンポ（BPM）の指定

**Q: BPMって何？**

→ テンポの速さを示す数値。**Beats Per Minute（1分間の拍数）**の略。数字が大きいほど速い。

#### BPMの感じ方ガイド

| BPM範囲 | 感じ方 | 具体例 |
|---------|--------|--------|
| **50-70** | とてもゆっくり | 子守唄、瞑想音楽 |
| **70-90** | ゆったり、しっとり | バラード、Lo-fi、ブルース |
| **90-110** | リラックス、作業用 | カフェミュージック、ジャズ |
| **110-130** | 標準的な速さ | ポップス、ロック |
| **130-150** | 少し速め、エネルギッシュ | ダンスミュージック、ハウス |
| **150+** | 速い、ノリノリ | EDM、ドラムンベース、メタル |

#### ジャンル別推奨BPM

**表5-3: ジャンル別BPM早見表**

| ジャンル | 推奨BPM範囲 | 典型的なBPM | 例 |
|----------|-------------|-------------|-----|
| **Ballad** | 60-80 | 70 | `70 BPM, slow ballad` |
| **Blues** | 60-90 | 75 | `75 BPM, blues` |
| **Lo-fi Hip Hop** | 70-90 | 80 | `80 BPM, lo-fi` |
| **Jazz** | 80-120 | 100 | `100 BPM, smooth jazz` |
| **Pop** | 110-130 | 120 | `120 BPM, upbeat pop` |
| **Rock** | 120-140 | 130 | `130 BPM, rock` |
| **House** | 120-130 | 125 | `125 BPM, house` |
| **Hip-Hop/Trap** | 140-150 | 145 | `~145 BPM, trap` |
| **Techno** | 120-135 | 128 | `128 BPM, driving techno` |
| **Drum & Bass** | 160-180 | 170 | `170 BPM, drum and bass` |

#### BPM指定の方法

**方法1: 数値指定（推奨）**

```
120 BPM
~145 BPM
```

**方法2: 意味的指定**

- **slow**: ゆっくり（70-80 BPM相当）
- **moderate**: 中程度（100-110 BPM相当）
- **upbeat**: アップテンポ（120-130 BPM相当）
- **fast**: 速い（140-150 BPM相当）

**重要**: BPMは単独では効果薄。ジャンル・ムード・楽器と**組み合わせて**指定する[2][11]。

#### BPM指定の実例

**例1: スローバラード**

```
Style: Ballad, melancholic
Instruments: Piano, strings
Tempo: 70 BPM
```

**期待される結果**: ゆったりとした切ないバラード。じっくりと感情を表現。

---

**例2: 標準的なポップス**

```
Style: Pop, uplifting
Instruments: Acoustic guitar, synths
Tempo: 120 BPM
```

**期待される結果**: 心地よい速さのポップス。歌いやすく、ノリやすい。

---

**例3: 激しいトラップ**

```
Style: Trap, intense
Instruments: 808 bass, heavy drums
Tempo: ~145 BPM
```

**期待される結果**: 速めでエネルギッシュなトラップ。ワークアウトに最適。

---

**図5-1: BPMと感じ方の関係**

```
50   60   70   80   90   100  110  120  130  140  150  160  170  180
|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
      ↓                    ↓              ↓              ↓         ↓
   子守唄             Lo-fi          ポップス        トラップ   D&B
   バラード          ジャズ          ロック          EDM
```

---

## 6. ネガティブプロンプト - 不要な要素を除外する

意図しない要素の混入を防ぐ「ネガティブプロンプト」の使い方を解説する。Suno v5では除外指示の精度が大幅向上し、初心者でも意図通りの結果を得やすくなった[4][5]。

### 6-1. ネガティブプロンプトとは？

**Q: ネガティブプロンプトって何？**

→ 「こういう要素は入れないで」という除外指示。ポジティブプロンプト（「これを入れて」）と対になる概念。

#### なぜ必要？

| 問題 | 原因 | ネガティブプロンプトによる解決 |
|------|------|-------------------------------|
| **意図しないボーカルが入る** | デフォルトで歌声が生成される | `no vocals`, `instrumental only` |
| **ギターの音が邪魔** | ジャンルのデフォルトにギターが含まれる | `no guitars` |
| **重すぎるドラム** | ロックジャンルで自動的に追加 | `no heavy drums`, `minimal percussion` |
| **電子音が嫌** | EDM要素が混入 | `no electronic synths`, `no EDM elements` |

**v5での改善**: 従来版（v4.5）では除外指示が不安定だったが、v5ではパース精度とレンダリング精度の改善により、**高精度で除外が実行**される[4]。

### 6-2. 効果的な除外の書き方

#### ✅ 良い例（明確で具体的）

**例1: ボーカル完全除外**

```
Instrumental only, no vocals.
```

**効果**: 歌声を完全に除外し、楽器だけの楽曲を生成。

---

**例2: ギターだけ除外**

```
Upbeat pop with drums and bass, no guitars.
```

**効果**: ポップスの構成はそのままに、ギターだけを除外。ドラムとベースは残る。

---

**例3: 808ベースのみ除外**

```
Trap beat with piano and synths, no 808s.
```

**効果**: トラップの要素は残しつつ、重低音の808ベースだけを除外。

---

#### ❌ 悪い例（曖昧で効果薄）

**例1: 条件が複雑**

```
Without singing unless background only.
```

**問題**: 条件分岐（「〜の場合は除く」）は解釈困難。単純な除外指示に変更すべき。

**改善**: `no lead vocals, background vocals only`

---

**例2: 抽象的すぎ**

```
No sounds that are bad.
```

**問題**: 「bad（悪い）」は主観的で、AIには判断不可。

**改善**: 具体的な楽器やスタイルを除外（例: `no distortion`, `no heavy drums`）

---

**例3: 代替が不明**

```
Not like rock.
```

**問題**: 「ロックじゃない」だけでは、何にすべきか不明。

**改善**: ポジティブな指示を追加（例: `Pop, no distortion, no heavy guitars`）

---

### 6-3. ジャンル別よくある除外

**表6-1: ジャンル別推奨除外**

| ジャンル | 推奨除外 | 理由 | プロンプト例 |
|----------|----------|------|--------------|
| **EDM** | `no acoustic instruments` | 電子音のみにしたい | `EDM, high energy, synths, no acoustic guitar, no piano` |
| **Rock** | `no electronic synths` | 生楽器のみにしたい | `Rock, energetic, electric guitar, drums, no synths` |
| **Ballad** | `no drums, no fast tempo` | 静かな雰囲気を保ちたい | `Ballad, melancholic, piano, no drums, slow` |
| **Instrumental** | `no vocals` | 歌声なし | `Jazz, instrumental only, no vocals` |
| **Acoustic** | `no electronic elements` | アコースティックのみ | `Folk, acoustic guitar, no electronic synths` |
| **Hip-Hop（Lofi）** | `no heavy bass, no trap elements` | 軽めのLofi | `Lo-fi Hip Hop, chill, piano, no heavy 808 bass` |

### 6-4. 高度なネガティブプロンプト戦略

#### 戦略1: レイヤー化（ポジティブ + ネガティブ）

ポジティブな指示とネガティブな指示を組み合わせることで、より精密な制御が可能[4]。

```
Acoustic guitar focus, no distortion, clear vocals.
```

**効果**:
- **ポジティブ**: アコースティックギター、クリアなボーカル
- **ネガティブ**: ディストーション（歪み）なし
- **結果**: 透明感のあるアコースティックサウンド

---

#### 戦略2: 精密な除外（部分的除外）

楽器全体ではなく、特定の要素だけを除外[4]。

```
No lead guitar solo
```

**効果**: リードギターのソロだけを除外。リズムギターは残る。

---

#### 戦略3: ジャンル特有の除外

ジャンルごとによくある「邪魔な要素」を事前に除外[4][5]。

**EDM**: `no hi-hats` → ハイハットの細かいリズムを除外し、よりシンプルに

**Rock**: `no distortion` → クリーンなロックサウンドに

**Hip-hop**: `no 808s` → 重低音を除外し、軽めのヒップホップに

---

### 6-5. トラブルシューティング

#### 問題1: ボーカルが消えない

**解決策1**: `instrumental only`を試す

```
Lo-fi Hip Hop, instrumental only, no vocals, piano, soft bass
```

**解決策2**: それでも残る場合は、Stemsエクスポート機能を使用

Sunoの「Stems」機能でボーカルと楽器を分離し、ボーカルトラックを削除。（Pro/Premierプラン限定）

---

#### 問題2: ミックスが空っぽに感じる

**原因**: 除外しすぎて楽器が少なくなった

**解決策**:
1. 除外を1つずつ減らす
2. ポジティブな指示を明確に追加

**改善例**:
```
# 除外しすぎ
Jazz, no piano, no bass, no drums, saxophone only

# 改善後
Jazz, smooth saxophone lead, soft piano, gentle bass
```

---

#### 問題3: 除外が効かない

**原因**: 曖昧な指示、または複数の矛盾する指示

**解決策**:
1. 具体的な楽器名や要素名を使用
2. 1つずつ除外して効果を確認

**改善例**:
```
# 曖昧
Pop, no bad sounds

# 具体的
Pop, no distortion, no heavy drums, no electronic synths
```

---

**図6-1: ネガティブプロンプトの効果（概念図）**

```
[Before - ネガティブプロンプトなし]
Pop + デフォルト要素（Guitar, Synths, Drums, Vocals）
→ すべての要素が含まれる

[After - ネガティブプロンプトあり]
Pop + デフォルト要素 - "no guitars, no synths"
→ Drums, Vocalsのみ残る
```

---

## 7. 初心者が避けるべき7つのミス

よくある失敗とその解決策を事前に知ることで、試行錯誤の時間を短縮できる[5][12]。

### ミス1: 曖昧なプロンプト

#### ❌ 悪い例

```
happy song
```

**問題点**:
- ジャンル不明（Pop? Rock? EDM?）
- 楽器不明
- テンポ不明

**結果**: AIが勝手に解釈し、意図と全く違う曲ができる可能性が高い。

---

#### ✅ 良い例

```
Pop, uplifting, acoustic guitar, 120 BPM
```

**改善点**:
- ジャンル: Pop
- 感情: uplifting
- 楽器: acoustic guitar
- テンポ: 120 BPM

**結果**: 期待値が明確で、意図通りの結果を得やすい。

---

### ミス2: 情報過多

#### ❌ 悪い例

```
rock pop jazz electronic with guitar piano drums bass synths vocals heavy 808s fast tempo
```

**問題点**:
- 10個以上の要素（ジャンル4種、楽器7種）
- 矛盾（rock + electronic、fast + heavy）

**結果**: AIが混乱し、ごちゃ混ぜの楽曲ができる。

---

#### ✅ 良い例

```
Indie Rock, melancholic, electric guitar, 120 BPM
```

**改善点**:
- ジャンル: 1種（Indie Rock）
- 感情: 1つ（melancholic）
- 楽器: 1種（electric guitar）
- テンポ: 明確

**推奨**: 4-7個のディスクリプタに絞る[3][7]。

---

### ミス3: 矛盾する指示

#### ❌ 悪い例

**例1**: `fast slow` → 速いのか遅いのか不明

**例2**: `dark cheerful` → 暗いのか明るいのか不明

**例3**: `melancholic uplifting` → 憂鬱なのか前向きなのか不明

---

#### ✅ 良い例

どちらか一方に決める。

- **速い**: `Rock, energetic, fast tempo`
- **遅い**: `Ballad, melancholic, slow tempo`
- **暗い**: `Ambient, dark, tense`
- **明るい**: `Pop, cheerful, uplifting`

---

### ミス4: ジャンルを3種以上指定

#### ❌ 悪い例

```
Pop Rock Jazz Hip-Hop
```

**問題点**: 4種類のジャンルは混乱の原因。各ジャンルの特徴が薄まる。

---

#### ✅ 良い例

**1種類**:
```
Pop
```

**2種類（ハイブリッド）**:
```
Pop Rock
```

**推奨**: Suno v5では**1-2種まで**が推奨[2][8]。

---

### ミス5: メタタグを使わない

#### ❌ 悪い例

```
Walking down the empty street
Looking for a place to be
We are alive, we are free
Dancing in the melody
Shadows dancing in the night
Everything will be alright
We are alive, we are free
Dancing in the melody
```

**問題点**: どこがバース、どこがコーラスか不明。AIが構造を誤解する可能性。

---

#### ✅ 良い例

```
[Verse 1]
Walking down the empty street
Looking for a place to be

[Chorus]
We are alive, we are free
Dancing in the melody

[Verse 2]
Shadows dancing in the night
Everything will be alright

[Chorus]
We are alive, we are free
Dancing in the melody
```

**改善点**: メタタグで構造を明示。AIが正しく解釈できる。

---

### ミス6: 即座の完璧を期待

#### ❌ 思考

「一度で完璧な曲ができるはず」

**問題点**: AIは試行錯誤が必要。最初から完璧を求めると失望する。

---

#### ✅ 思考

「複数バージョンを生成し、ベストを選ぶ」

**推奨アプローチ**:
1. 同じプロンプトで2-3バージョン生成
2. 各バージョンの良い部分を比較
3. 必要に応じてプロンプトを微調整
4. 再度生成

**現実**: プロの楽曲も複数テイクから選ばれる。AIも同じ。

---

### ミス7: プロンプトを記録しない

#### ❌ 行動

成功したプロンプトを忘れる。

**問題点**:
- 同じ結果を再現できない
- 何が効いたのか不明

---

#### ✅ 行動

スプレッドシートやメモで記録する。

**記録例**（Googleスプレッドシート）:

| 日付 | プロンプト | 結果 | 評価 | メモ |
|------|-----------|------|------|------|
| 2025-10-01 | `Pop, uplifting, acoustic guitar, 120 BPM` | 明るいポップス | ★★★★☆ | 朝向け、ギター良し |
| 2025-10-02 | `Ballad, melancholic, piano, 70 BPM` | 切ないバラード | ★★★★★ | 完璧！失恋ソング |
| 2025-10-03 | `Rock, energetic, electric guitar, 130 BPM` | パワフルロック | ★★★☆☆ | ドラムが強すぎ |

**メリット**:
- 成功パターンを再利用できる
- 改善点が明確になる
- プロンプトライブラリが蓄積される

---

**表7-1: ミス×解決策チェックリスト**

| ミス | チェック項目 | 解決策 |
|------|--------------|--------|
| ✓ 曖昧なプロンプト | ジャンル・感情・楽器が明確か？ | 3ステップフレームワークを使う |
| ✓ 情報過多 | 要素が4-7個以内か？ | 最小限に絞る |
| ✓ 矛盾する指示 | fast/slow等の矛盾がないか？ | どちらか一方に決める |
| ✓ ジャンル過多 | ジャンルが1-2種か？ | 3種以上は避ける |
| ✓ メタタグなし | [Verse], [Chorus]を使っているか？ | 構造を明示 |
| ✓ 即座の完璧期待 | 複数バージョンを試したか？ | 試行錯誤を楽しむ |
| ✓ 記録なし | プロンプトを記録しているか？ | スプレッドシートで管理 |

---

## 8. トラブルシューティング - よくある問題と解決策

「うまくいかない」ときの対処法を、問題別に解説する[4][5][12]。

### 問題1: 意図しないボーカルが入る

**症状**: 楽器だけの曲を作りたいのに、歌声が入ってしまう。

**原因**: Sunoはデフォルトでボーカルを生成する。

**解決策**:

**Step 1**: `instrumental only, no vocals`を追加

```
Jazz, serene, saxophone, piano, instrumental only, no vocals
```

**Step 2**: それでも残る場合は、Stemsエクスポート機能を使用（Pro/Premierプラン限定）

1. 楽曲生成後、「Stems」ボタンをクリック
2. ボーカルトラックと楽器トラックが分離される
3. 楽器トラックのみをダウンロード

---

### 問題2: ジャンルが混ざる

**症状**: ロックを指定したのに、ポップスやジャズの要素が混ざる。

**原因**: 複数ジャンル指定、または曖昧な指示。

**解決策**:

**Step 1**: ジャンルを1-2種に絞る

```
# 悪い例
Rock Pop Jazz Electronic

# 良い例
Rock
```

**Step 2**: ネガティブプロンプトで不要なジャンル要素を除外

```
Rock, energetic, electric guitar, no electronic synths, no jazz elements
```

---

### 問題3: テンポが合わない

**症状**: 指定したテンポよりも速い/遅い楽曲ができる。

**原因**: BPM指定が曖昧、またはジャンルのデフォルトテンポと矛盾。

**解決策**:

**Step 1**: 具体的なBPM数値を指定

```
# 曖昧
Pop, fast

# 具体的
Pop, 140 BPM
```

**Step 2**: BPMとジャンルの相性を確認

| ジャンル | 典型的なBPM | 相性の良いBPM範囲 |
|----------|-------------|-------------------|
| Ballad | 60-80 | 70 BPM |
| Pop | 110-130 | 120 BPM |
| Rock | 120-140 | 130 BPM |
| Trap | 140-150 | ~145 BPM |

**Step 3**: テンポを繰り返し強調

```
Pop, upbeat, fast tempo, 140 BPM, high energy
```

---

### 問題4: 楽曲が単調

**症状**: 最初から最後まで同じ雰囲気で、変化がない。

**原因**: 構造指示なし。メタタグを使っていない。

**解決策**:

**Step 1**: メタタグで構造を明示

```
[Verse 1]
...

[Chorus]
...

[Bridge]
...
```

**Step 2**: セクションごとに指示を変える

```
[Verse 1: Soft, piano only]
...

[Chorus: Full band, energetic]
...

[Bridge: Acoustic, reflective]
...
```

**Step 3**: 感情アークを設計

```
[Verse 1: Sad mood]
...

[Pre-Chorus: Hope building]
...

[Chorus: Triumphant]
...
```

---

### 問題5: 終わり方が不自然

**症状**: 楽曲が途中で突然終わる、または終わりが不明瞭。

**原因**: アウトロ指示なし。

**解決策**:

**Step 1**: `[Outro]`タグを追加

```
[Chorus]
...

[Outro]
(fade out)
```

**Step 2**: アウトロの内容を指定

```
[Outro]
(fade out with humming)
```

```
[Outro]
(repeat chorus, gradual fade)
```

```
[Outro]
(instrumental, piano only, 4 bars)
```

---

### 問題6: ムードが違う

**症状**: 「切ない」を指定したのに、明るい曲ができる。

**原因**: 感情語が不明瞭、または矛盾する指示。

**解決策**:

**Step 1**: 具体的な感情語を使用

```
# 曖昧
Sad song

# 具体的
Ballad, melancholic, piano, slow
```

**Step 2**: 感情語を繰り返す

プロンプトの最初と最後に同じ感情語を配置することで、AIが「雰囲気をロックイン」しやすくなる[6]。

```
melancholic, Ballad, piano, strings, slow tempo, melancholic
```

**Step 3**: ジャンルと感情の相性を確認

| 感情 | 相性の良いジャンル |
|------|--------------------|
| melancholic | Ballad, Indie Folk, Blues |
| uplifting | Pop, Folk, Indie Pop |
| energetic | Rock, EDM, Hip-Hop |
| serene | Jazz, Ambient, Classical |

---

**表8-1: 問題×原因×解決策マトリックス**

| 問題 | 原因 | 解決策 |
|------|------|--------|
| ボーカルが入る | デフォルト設定 | `instrumental only, no vocals` |
| ジャンル混在 | 複数ジャンル指定 | 1-2種に絞る、ネガティブプロンプト |
| テンポ違い | BPM曖昧 | 具体的なBPM数値を指定 |
| 単調 | 構造指示なし | メタタグで[Verse], [Chorus]等を明示 |
| 不自然な終わり | アウトロなし | `[Outro] (fade out)`を追加 |
| ムード違い | 感情語不明瞭 | 具体的な感情語（melancholic等）を使用 |

---

## 9. 実践ワークショップ - 一緒に作ってみよう

ステップバイステップで1曲を完成させるワークショップ。実際の手順を追体験しながら、プロンプト作成の流れを理解しよう。

### 9-1. ゴール設定

**作りたいフィーリング**: 「爽やかな朝、新しい一日が始まる感じ」

**具体的なシーン**: 朝起きて、窓を開け、朝日を浴びながらコーヒーを飲む。前向きな気持ちで一日をスタート。

---

### 9-2. Step 1: ジャンル選び

**Q: どんなジャンルが合う？**

- 明るく元気 → **Pop**
- 自然な感じも欲しい → **Indie Pop**（インディーズ風のポップス）

**選択**: `Indie Pop`

---

### 9-3. Step 2: 感情選び

**Q: どんな感情を表現したい？**

- 前向き、高揚感 → **uplifting**

**選択**: `uplifting`

---

### 9-4. Step 3: 楽器選び

**Q: どんな音色が合う？**

- 温かく柔らかい → **Acoustic guitar**（アコースティックギター）

**選択**: `acoustic guitar`

---

### 9-5. Step 4: テンポ指定（オプション）

**Q: どれくらいの速さ？**

- 標準的なポップスの速さ → **115 BPM**

**選択**: `115 BPM`

---

### 9-6. プロンプト完成

```
Style: Indie Pop, uplifting, acoustic guitar, 115 BPM
```

---

### 9-7. 歌詞とメタタグ追加

次に、歌詞を追加し、メタタグで構造を指定する。

```
[Intro]
(instrumental, acoustic guitar, 8 bars)

[Verse 1]
Sun is rising, new day ahead
Feeling grateful for what I have
Birds are singing, sky is clear
Everything I need is right here

[Chorus]
It's a beautiful morning
Everything feels right
I'm ready for the day
Bring on the light

[Verse 2]
Coffee brewing, gentle breeze
Life is full of simple pleasures
Breathing in, letting go
This is all I need to know

[Chorus]
It's a beautiful morning
Everything feels right
I'm ready for the day
Bring on the light

[Outro]
(fade out with humming, acoustic guitar)
```

---

### 9-8. 生成と評価

**Sunoで生成**:
1. 「Custom Mode」を選択
2. 「Style of Music」欄に: `Indie Pop, uplifting, acoustic guitar, 115 BPM`
3. 「Lyrics」欄に: 上記の歌詞とメタタグをコピー&ペースト
4. 「Create」ボタンをクリック
5. 数秒待つ

**期待される結果**:
- 明るくポジティブな雰囲気
- アコースティックギターの柔らかい音色
- 朝のルーティンに最適
- 軽快なテンポで心地よい目覚めを演出

---

### 9-9. もし意図と違った場合の調整

#### ケース1: テンポが速すぎる

**問題**: 115 BPMの指定なのに、もっと速く感じる。

**調整**:
```
Style: Indie Pop, uplifting, acoustic guitar, 100 BPM
```

---

#### ケース2: 楽器が多すぎる

**問題**: ドラムやベースが強く、アコースティックな雰囲気が薄い。

**調整**:
```
Style: Indie Pop, uplifting, acoustic guitar, 115 BPM, no heavy drums, no bass
```

---

#### ケース3: ボーカルが強すぎる

**問題**: 歌声が前面に出すぎて、楽器が聞こえにくい。

**調整**:
```
Style: Indie Pop, uplifting, acoustic guitar, 115 BPM, soft vocal, acoustic focus
```

---

### 9-10. 調整のポイント

**1つずつ変更する**: 複数要素を同時に変えると、何が効いたか不明。

**記録する**: 各バージョンのプロンプトと結果を記録し、最適解を見つける。

**楽しむ**: 試行錯誤を楽しむ。完璧を求めず、プロセスを楽しもう。

---

**図9-1: ワークショップのフローチャート**

```
[1. ゴール設定] → 「爽やかな朝」
     ↓
[2. ジャンル選び] → Indie Pop
     ↓
[3. 感情選び] → uplifting
     ↓
[4. 楽器選び] → acoustic guitar
     ↓
[5. テンポ指定] → 115 BPM
     ↓
[6. プロンプト完成] → "Indie Pop, uplifting, acoustic guitar, 115 BPM"
     ↓
[7. 歌詞とメタタグ追加] → [Verse], [Chorus]等
     ↓
[8. Sunoで生成] → Create!
     ↓
[9. 評価] → 意図通り？
     ↓
[10. 調整（必要に応じて）] → プロンプト微調整 → 再生成
```

---

## 10. まとめ - 今日から始める3つのアクション

本記事で学んだことを実践に移すための具体的なアクションプランを提示する。

### アクション1: クイックスタートテンプレートを使う

最も簡単な始め方は、**3ステップフレームワーク**をそのまま使うこと。

**テンプレート**:
```
[ジャンル], [感情], [楽器]
```

**今すぐ試せる5つの例**:

1. **爽やかな朝**: `Pop, uplifting, acoustic guitar`
2. **切ない夜**: `Ballad, melancholic, piano`
3. **エネルギー爆発**: `Rock, energetic, electric guitar`
4. **リラックス**: `Jazz, serene, saxophone`
5. **集中作業**: `Ambient, minimal, soft pads, no vocals`

**やること**:
1. Sunoにアクセス（https://suno.com）
2. 上記のいずれか1つをコピー
3. 「Style of Music」欄にペースト
4. 「Create」ボタンをクリック
5. 結果を聴く

**所要時間**: 5分

---

### アクション2: 感情マップから1つ選んで試す

本記事の「3. 感情マップ」から、自分のフィーリングに近いパターンを1つ選び、そのままコピー&ペーストして生成。

**推奨パターン**（初心者向け）:

- **パターン1**: 爽やかな朝 → `Indie Pop, uplifting, acoustic guitar, 115 BPM`
- **パターン6**: 切ない別れ → `Ballad, melancholic, piano, strings, slow (80 BPM)`
- **パターン11**: リラックスタイム → `Jazz, serene, smooth saxophone, soft piano, 90 BPM`

**やること**:
1. 15パターンから1つ選ぶ
2. プロンプトをそのままコピー
3. Sunoの「Style of Music」欄にペースト
4. 歌詞は「Auto」モードで自動生成（歌詞を書くのが面倒な場合）
5. 「Create」ボタンをクリック

**所要時間**: 5分

---

### アクション3: 成功プロンプトを記録する

試行錯誤の過程で見つけた「良いプロンプト」を記録し、再利用可能なライブラリを作る。

**推奨ツール**:
- Googleスプレッドシート
- Notion
- メモアプリ

**記録フォーマット**:

| 日付 | フィーリング | プロンプト | 結果 | 評価 | メモ |
|------|--------------|-----------|------|------|------|
| 2025-10-07 | 爽やかな朝 | `Pop, uplifting, acoustic guitar, 115 BPM` | 明るいポップス | ★★★★☆ | ギター良し、少し速め |
| 2025-10-08 | 切ない夜 | `Ballad, melancholic, piano, 70 BPM` | 静かなバラード | ★★★★★ | 完璧！ |

**やること**:
1. Googleスプレッドシートを開く
2. 上記のフォーマットをコピー
3. 生成した楽曲ごとに記録
4. 評価（★1-5）を付ける
5. メモ欄に気づきを記入

**所要時間**: 各生成後2分

---

### 最終メッセージ

**音楽知識ゼロでも、「こんな気分」という感情を言語化できれば、誰でもプロ品質の楽曲を生成できる。**

本記事で学んだ3つの核心：

1. **3ステップフレームワーク**: ジャンル + 感情 + 楽器
2. **メタタグ**: [Verse], [Chorus]で構造制御
3. **トライ&エラー**: 完璧を求めず、試行錯誤を楽しむ

**今日からあなたもAI音楽クリエイターだ。まずは1曲、作ってみよう。**

---

**図10-1: クイックリファレンスカード**

```
┌─────────────────────────────────────────────────┐
│  Suno v5 クイックリファレンスカード           │
├─────────────────────────────────────────────────┤
│ 【3ステップフレームワーク】                    │
│ [ジャンル] + [感情] + [楽器]                   │
│                                                  │
│ 例: Pop, uplifting, acoustic guitar             │
├─────────────────────────────────────────────────┤
│ 【基本メタタグ】                               │
│ [Intro] - イントロ                             │
│ [Verse] - バース（物語）                       │
│ [Chorus] - コーラス（サビ）                    │
│ [Bridge] - ブリッジ（変化）                    │
│ [Outro] - アウトロ（終わり）                   │
├─────────────────────────────────────────────────┤
│ 【感情ワード】                                 │
│ ポジティブ: uplifting, joyful, energetic       │
│ ネガティブ: melancholic, somber, wistful       │
│ ニュートラル: dreamy, serene, mysterious       │
├─────────────────────────────────────────────────┤
│ 【楽器】                                       │
│ 温かい: acoustic guitar, piano                 │
│ かっこいい: electric guitar, drums             │
│ 大人: saxophone, warm Rhodes piano             │
├─────────────────────────────────────────────────┤
│ 【BPM】                                        │
│ 遅い: 70 BPM (バラード)                        │
│ 標準: 120 BPM (ポップス)                       │
│ 速い: 145 BPM (トラップ)                       │
├─────────────────────────────────────────────────┤
│ 【ネガティブプロンプト】                       │
│ ボーカルなし: no vocals, instrumental only     │
│ ギターなし: no guitars                         │
│ ドラムなし: no drums                           │
└─────────────────────────────────────────────────┘
```

（印刷して手元に置いておくと便利！）

---

## 付録A: 用語集（音楽知識不要版）

音楽理論を知らない読者のための、平易な用語解説。

| 用語 | 意味（平易な説明） | 具体例 |
|------|---------------------|--------|
| **ジャンル** | 音楽のスタイル | ポップス、ロック、ジャズ、バラード |
| **BPM** | テンポの速さの単位。数字が大きいほど速い | 70 BPM（遅い）、120 BPM（標準）、145 BPM（速い） |
| **ビブラート** | 音を震わせる歌唱技法。感情表現に使われる | 「あ〜〜〜〜」と声を震わせる |
| **レガート** | 音を滑らかに繋げる演奏方法 | 「た〜〜〜」と音を伸ばして繋げる |
| **スタッカート** | 音を短く切る演奏方法 | 「タ・タ・タ」と短く切る |
| **バース（Verse）** | 歌の物語部分。通常複数回繰り返される | 1番、2番、3番等 |
| **コーラス（Chorus）** | 歌の最も印象的な部分。サビ | 「ここがサビ！」という盛り上がる部分 |
| **ブリッジ（Bridge）** | 歌の途中で変化をつける部分 | 転調したり、リズムが変わったり |
| **イントロ（Intro）** | 楽曲の始まりの部分 | 歌が始まる前の楽器だけの演奏 |
| **アウトロ（Outro）** | 楽曲の終わりの部分 | 歌が終わった後の余韻 |
| **メタタグ** | Sunoへの指示を[  ]で囲んだもの | [Verse], [Chorus]等 |
| **プロンプト** | AIへの指示文 | 「Pop, uplifting, acoustic guitar」 |
| **ネガティブプロンプト** | 「〜を入れないで」という除外指示 | 「no vocals」「no guitars」 |
| **アコースティック** | 電気を使わない楽器。生楽器 | アコースティックギター、ピアノ |
| **エレクトリック** | 電気で音を増幅する楽器 | エレキギター、電子キーボード |
| **シンセ（Synth）** | シンセサイザーの略。電子音を作る楽器 | 未来的な「ピロピロ」という音 |
| **808** | ローランドTR-808という有名なドラムマシンの名前。重低音が特徴 | Hip-Hopの「ズンズン」という低音 |

---

## 付録B: ジャンル×感情×楽器の組み合わせマトリックス

よく使われる組み合わせを一覧化。迷ったらこの表から選ぶと失敗しにくい。

**表B-1: 推奨組み合わせマトリックス**

| フィーリング | ジャンル | 感情ワード | 楽器 | BPM | プロンプト例 |
|--------------|----------|-----------|------|-----|--------------|
| 爽やかな朝 | Indie Pop | uplifting | acoustic guitar | 115 | `Indie Pop, uplifting, acoustic guitar, 115 BPM` |
| 切ない夜 | Ballad | melancholic | piano, strings | 70 | `Ballad, melancholic, piano, strings, 70 BPM` |
| エネルギー爆発 | Rock | energetic | electric guitar, drums | 130 | `Rock, energetic, electric guitar, drums, 130 BPM` |
| リラックス | Jazz | serene | saxophone, piano | 90 | `Jazz, serene, saxophone, soft piano, 90 BPM` |
| 集中作業 | Ambient | minimal | soft pads | 100 | `Ambient, minimal, soft pads, no vocals, 100 BPM` |
| ロマンティック | Jazz Ballad | romantic | saxophone, piano | 85 | `Jazz Ballad, romantic, saxophone, warm Rhodes piano, 85 BPM` |
| 激しいワークアウト | Trap Metal | intense | distorted guitar, 808 | 145 | `Trap Metal, intense, distorted guitar, 808 bass, ~145 BPM` |
| 神秘的な森 | Celtic | mysterious | flute, harp | 95 | `Celtic, mysterious, flute, harp, strings, 95 BPM` |
| 夏のビーチ | Tropical House | cheerful | steel drums | 110 | `Tropical House, cheerful, steel drums, acoustic guitar, 110 BPM` |
| 深夜の孤独 | Lo-fi Hip Hop | introspective | piano, 808 | 70 | `Lo-fi Hip Hop, introspective, piano, soft 808 bass, 70 BPM` |

---

## 付録C: 公式リソースリンク集

さらに学びたい方へ、公式ドキュメントとコミュニティリソースを紹介。

### 公式ドキュメント（一次情報）

| リソース | URL | 内容 |
|---------|-----|------|
| **Suno v5公式ヘルプ** | https://help.suno.com/en/articles/8105153 | v5の公式機能紹介 |
| **V4.5 Better Prompts in Lyrics** | https://help.suno.com/en/articles/5782977 | プロンプトの書き方（v4.5、v5にも適用） |
| **V4.5 Detailed Style Instructions** | https://help.suno.com/en/articles/5782849 | スタイル指定の詳細 |
| **Suno Model Timeline** | https://help.suno.com/en/articles/5782721 | モデルの進化履歴 |

### コミュニティリソース（二次情報）

| リソース | URL | 内容 |
|---------|-----|------|
| **Suno AI Wiki（日本語）** | https://ai.suno.jp/ | 2,150+のプロンプト要素を日本語で検索 |
| **Suno AI Wiki（英語）** | https://sunoaiwiki.com/ | メタタグリスト、チュートリアル |
| **Jack Righteous ガイド集** | https://jackrighteous.com/ | ネガティブプロンプト、初心者ミス等 |

### 学習リソース

| リソース | 内容 |
|---------|------|
| **SHIFT AI TIMES** | Suno AIのプロンプトの書き方（日本語） |
| **Medium - Travis Nicholson** | Complete List of Prompts & Styles（英語） |
| **Reddit - r/SunoAI** | コミュニティディスカッション、実例共有 |

---

## 出典一覧

[1] Suno公式ヘルプ - Introducing v5: https://help.suno.com/en/articles/8105153
[2] WebSearch結果統合 - Suno v5機能比較（複数ソース）
[3] Vozart.ai - How to Prompt Suno: https://vozart.ai/blog/how-to-prompt-suno
[4] Jack Righteous - Negative Prompting in Suno v5 Guide: https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/negative-prompting-suno-v5-guide
[5] Jack Righteous - 7 Beginner Mistakes to Avoid: https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/beginner-mistakes-with-suno-ai
[6] Suno AI Wiki（日本語）- プロンプト要素集: https://ai.suno.jp/
[7] Musicful.ai - 50+ Best Suno Prompts: https://www.musicful.ai/music-tips/suno-prompts/
[8] WebSearch結果 - Suno v5 best practices（複数ソース統合）
[9] SHIFT AI TIMES - Suno AIのプロンプトの書き方: https://shift-ai.co.jp/blog/22691/
[10] Suno Wiki - Meta Tags List: https://sunoaiwiki.com/resources/2024-05-13-list-of-metatags/
[11] WebSearch結果 - Suno BPM specification（複数ソース統合）
[12] WebSearch結果 - Suno troubleshooting（複数ソース統合）

---

**最終更新**: 2025-10-07
**文字数**: 約12,050字
**執筆**: AI Music Research

---

*このガイドが、あなたの音楽創作の第一歩になることを願っています。質問やフィードバックがあれば、Sunoコミュニティで共有してください。Happy Music Making!*
