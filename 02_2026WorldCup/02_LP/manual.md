# FIFA ワールドカップ 2026 LP 制作マニュアル

---

## 1. 概要

| 項目 | 内容 |
|---|---|
| ファイル名 | `worldcup2026_lp.html` |
| 格納場所 | `/Desktop/soccer/2026WorldCup/` |
| 制作日 | 2026年6月1日 |
| 最終更新 | 2026年6月1日（選手セクション・追従CTA追加） |
| 技術スタック | HTML5 / CSS3 / Vanilla JavaScript（外部ライブラリなし） |
| 対応デバイス | PC・スマートフォン（レスポンシブ対応） |

### ファイル構成

```
2026WorldCup/
├── worldcup2026_lp.html   # LP本体
├── manual.md              # 本マニュアル（Markdown）
├── manual.html            # 本マニュアル（ブラウザ表示用）
└── images/                # 選手画像（Wikimedia Commons CC ライセンス）
    ├── mbappe.jpg
    ├── vinicius.jpg
    ├── bellingham.jpg
    ├── messi.jpg
    ├── ronaldo.jpg
    ├── yamal.jpg
    ├── haaland.jpg
    └── kubo.png
```

---

## 2. 参考情報・出典

| 情報源 | URL | 取得内容 |
|---|---|---|
| FIFA 公式サイト（日本語） | https://www.fifa.com/ja/tournaments/mens/worldcup/canadamexicousa2026/articles/fifa-world-cup-2026-hosts-cities-dates-usa-mexico-canada-ja | 大会概要・開催都市・日程（JSレンダリングのため直接取得不可、Web検索で補完） |
| FIFA 公式サイト（英語） | https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026 | 大会フォーマット・開催都市・試合スケジュール |
| Wikipedia（日本語） | https://ja.wikipedia.org/wiki/2026_FIFA%E3%83%AF%E3%83%BC%E3%83%AB%E3%83%89%E3%82%AB%E3%83%83%E3%83%97 | 大会詳細・参加国数・試合数 |
| Goal.com 日本 | https://www.goal.com/jp/リスト/canada-mexico-usa-world-cup-2026-information/blt6c7b867a121500ab | 開幕日・キックオフ時間・出場国情報 |
| Wikimedia Commons | https://commons.wikimedia.org/ | 選手画像（CC ライセンス） |

> **備考**: FIFA 公式サイトは JavaScript による動的レンダリングのため `WebFetch` での直接取得ができなかった。`WebSearch` で情報を収集し補完した。

---

## 3. LP に反映した大会データ

| データ項目 | 内容 |
|---|---|
| 開催国 | アメリカ（主）・メキシコ・カナダ（3カ国共同開催・史上初） |
| 開催期間 | 2026年6月11日 〜 7月19日（39日間） |
| 参加チーム数 | 48カ国（従来32から拡大・史上最多） |
| 総試合数 | 104試合（グループ72 + 決勝T32） |
| 開催都市数 | 16都市（USA 11 / Mexico 3 / Canada 2） |
| グループ数 | 12グループ × 4チーム |
| 決勝トーナメント進出 | 各グループ上位2チーム + 3位グループ上位8チーム = 32チーム |
| 開幕戦会場 | エスタディオ・アステカ（メキシコシティ） |
| 決勝会場 | メトライフ・スタジアム（ニューヨーク / ニュージャージー） |
| ドロー開催 | 2025年12月5日、ケネディ・センター（ワシントンD.C.） |

---

## 4. LP セクション構成と実装内容

### 4-1. ナビゲーション（固定ヘッダー）

- `position: fixed` で画面上部に固定
- `backdrop-filter: blur` でスクロール時の透過エフェクト
- 各セクションへのアンカーリンク（概要 / 形式 / 開催都市 / 日程 / 日本代表 / 注目選手 / 詳細を見る）
- スマートフォン時は非表示（`display: none`）

---

### 4-2. Hero セクション

**目的**: ファーストビューで大会の規模感とワクワク感を伝える

| 実装要素 | 詳細 |
|---|---|
| 背景グラデーション | `radial-gradient` 2層 + `linear-gradient` でW杯カラー（青・赤）を演出 |
| ピッチグリッド | `repeating-linear-gradient` でサッカーピッチの芝目を再現（opacity 5%） |
| カウントダウンタイマー | JavaScript `setInterval` で1秒毎に更新。開幕日（2026/6/11）まで残り日数・時間・分・秒を表示 |
| 開幕後の処理 | `diff <= 0` 判定で「⚽ 開幕！」テキストに自動切り替え |
| フェードインアニメーション | `@keyframes fadeUp` + `animation-delay` で要素を順番に表示 |

---

### 4-3. Stats バンド

**目的**: 4つの数字で大会の規模を瞬時に伝える

| 表示内容 | 数値 |
|---|---|
| 参加国数 | 48カ国 |
| 総試合数 | 104試合 |
| 開催都市数 | 16都市 |
| 共同開催国数 | 3カ国 |

- 背景に `linear-gradient`（赤→青）でW杯カラー帯
- グリッドの区切り線は `background: rgba(255,255,255,0.15)` で1pxライン
- ホバーで背景色が暗くなるインタラクション

---

### 4-4. Format セクション

**目的**: 新フォーマット（48チーム・ラウンド32）を分かりやすく説明

- 左: 3ステップのフロー（グループステージ → ラウンド32 → 決勝）
- 右: 数字カード6枚（グループ数・1グループ人数・グループ戦試合数・決勝T試合数・優勝までの試合数）
- `fv-card.accent` でワイドカードを実装（`grid-column: 1 / -1`）

---

### 4-5. Cities セクション

**目的**: 16開催都市を3カ国に色分けして一覧表示

- 国別カード3枚（USA / Mexico / Canada）に都市数・試合数を掲載
- 16都市タグを `auto-fill` グリッドで可変列表示
- 開幕戦・決勝会場はバッジ（`city-games`）でハイライト

---

### 4-6. Schedule セクション

**目的**: 大会の流れをタイムラインで視覚化

| マイルストーン | 日付 | バッジカラー |
|---|---|---|
| 開幕戦 | 2026/6/11 | ゴールド |
| グループステージ | 6/11〜6/27 | ブルー |
| 決勝トーナメント | 6月下旬〜7月上旬 | レッド |
| 決勝 | 2026/7/19 | グラデーション（ゴールド） |

- 縦ライン: `::before` 疑似要素 + `linear-gradient`（金→青→金）
- ドット: `position: absolute` + `box-shadow` でグロー効果

---

### 4-7. Japan セクション

**目的**: 日本人ユーザーへの感情訴求・日本代表の情報提供

- 中央の円形バッジに `@keyframes pulse` でアニメーション（box-shadow の拡縮）
- アジア枠の拡大（8.5カ国）・出場決定・ベスト8目標を明記

---

### 4-8. Players セクション（注目選手）★追加

**目的**: 世界のスター選手を画像とセットで紹介し、滞在時間を伸ばす

| 選手名 | 国 | ポジション | 画像ファイル |
|---|---|---|---|
| キリアン・ムバッペ | 🇫🇷 フランス | FW | `images/mbappe.jpg` |
| ヴィニシウス Jr. | 🇧🇷 ブラジル | FW | `images/vinicius.jpg` |
| ジュード・ベリンガム | 🏴󠁧󠁢󠁥󠁮󠁧󠁿 イングランド | MF | `images/bellingham.jpg` |
| リオネル・メッシ | 🇦🇷 アルゼンチン | FW | `images/messi.jpg` |
| C・ロナウド | 🇵🇹 ポルトガル | FW | `images/ronaldo.jpg` |
| ラミン・ヤマル | 🇪🇸 スペイン | FW | `images/yamal.jpg` |
| A・ハーランド | 🇳🇴 ノルウェー | FW | `images/haaland.jpg` |
| 久保 建英 | 🇯🇵 日本 | MF | `images/kubo.png` |

**カード実装の詳細:**

- `aspect-ratio: 3 / 4` で縦長の選手カードを統一
- `object-fit: cover; object-position: top center` で顔を切り抜かずに表示
- `player-img-overlay`: 下部に `linear-gradient` でテキスト可読性を確保
- 左上: 国旗バッジ（`backdrop-filter: blur` で半透明）
- 右上: ポジションバッジ（FW / MF / DF）
- ホバー: カードが `translateY(-8px)` で浮き上がり、写真が `scale(1.06)` で拡大

**画像の取得方法:**

Wikimedia Commons からローカルダウンロード。ホットリンクが制限されているため `python3 urllib` でダウンロードして `images/` フォルダに保存。

> **注意**: Wikimedia の許可サムネイルサイズは `20 / 40 / 60 / 120 / 250 / 330 / 500 / 960 / 1280 / 1920 / 3840 px` のみ。`400px` などは HTTP 400 エラーになる。本 LP では `500px` を使用。

---

### 4-9. CTA セクション

**目的**: FIFA公式サイトへの誘導

- 背景に巨大な ⚽ 絵文字（`opacity: 0.03`）でテクスチャ感
- プライマリボタン: ゴールド背景 + `box-shadow` グロー
- セカンダリボタン: アウトライン

---

### 4-10. Sticky CTA（追従ボタン）★追加

**目的**: どのセクションを閲覧中でも FIFA 公式サイトへ誘導できるようにする

| 項目 | 内容 |
|---|---|
| 表示タイミング | Hero セクションをスクロールで抜けた瞬間 |
| 非表示タイミング | CTA セクションが画面内に入ったとき（重複防止） |
| 位置 | 画面右下固定（スマホは画面下部横幅いっぱい） |
| 遷移先 | https://www.fifa.com/ja/tournaments/mens/worldcup/canadamexicousa2026/articles/fifa-world-cup-2026-hosts-cities-dates-usa-mexico-canada-ja |
| ボタン文言 | ⚽ 詳細はこちら |

```javascript
const obs = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.target === hero)   cta.classList.toggle('show', !e.isIntersecting);
    if (e.target === ctaSec) cta.classList.toggle('show', !e.isIntersecting);
  });
}, { threshold: 0.2 });
obs.observe(hero);
obs.observe(ctaSec);
```

---

## 5. デザインシステム

### カラーパレット

| 変数名 | 値 | 用途 |
|---|---|---|
| `--gold` | `#FFD700` | 強調・タイトル・ボタン |
| `--red` | `#C8102E` | アクセント（W杯レッド） |
| `--blue` | `#1A6FD4` | アクセント（W杯ブルー）※`#003F88` から変更 |
| `--dark` | `#0A0A0F` | メイン背景 |
| `--mid` | `#12122A` | サブ背景 |
| `--accent` | `#00D4FF` | 補助アクセント |

### タイポグラフィ

- フォント: `Helvetica Neue`, `Arial`, `Hiragino Kaku Gothic ProN`（日本語対応）
- ヒーロー見出し: `clamp(3rem, 9vw, 8rem)` でビューポートに応じて可変
- グラデーションテキスト: `-webkit-background-clip: text` で実装

---

## 6. JavaScript 実装

### カウントダウンタイマー

```javascript
const target = new Date('2026-06-11T00:00:00');
setInterval(() => {
  const diff = target - new Date();
  if (diff <= 0) {
    // 開幕後は「⚽ 開幕！」に切り替え
    return;
  }
  const d = Math.floor(diff / 86400000);
  const h = Math.floor((diff % 86400000) / 3600000);
  const m = Math.floor((diff % 3600000) / 60000);
  const s = Math.floor((diff % 60000) / 1000);
  // DOM に反映
}, 1000);
```

### スクロールリビール

```javascript
const obs = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      obs.unobserve(e.target); // パフォーマンス最適化
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
```

- `IntersectionObserver` でビューポートに入った要素に `.visible` を付与
- CSS側で `.reveal` → `.reveal.visible` のトランジションを定義
- `obs.unobserve()` でアニメーション後は監視を解除（パフォーマンス最適化）

### Sticky CTA（追従ボタン）

```javascript
const cta    = document.getElementById('stickyCta');
const hero   = document.getElementById('hero');
const ctaSec = document.getElementById('cta');
const obs = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.target === hero)   cta.classList.toggle('show', !e.isIntersecting);
    if (e.target === ctaSec) cta.classList.toggle('show', !e.isIntersecting);
  });
}, { threshold: 0.2 });
obs.observe(hero);
obs.observe(ctaSec);
```

---

## 7. レスポンシブ対応

`@media (max-width: 768px)` で以下を調整:

| 対象 | PC | スマートフォン |
|---|---|---|
| ナビリンク | 表示 | 非表示 |
| Stats グリッド | 4列 | 2列 |
| Format / Japan / Cities | 2列 | 1列 |
| Hero タイトル | `clamp` で最大8rem | `clamp` で最小3rem |
| Players グリッド | 4列 | 2列 |
| Sticky CTA | 右下固定 | 画面下部横幅いっぱい |

---

## 8. 今後のカスタマイズポイント

| 改善案 | 実装方法 |
|---|---|
| 試合日程の詳細追加 | グループごとの対戦表を表形式で追加 |
| 日本代表の試合予定 | 確定次第タイムラインに追記 |
| 動画背景 | Hero の `.hero-bg` を `<video>` タグに置換 |
| OGP対応 | `<meta property="og:...">` タグを追加 |
| SNSシェアボタン | CTA セクションに Twitter/X・LINE ボタンを追加 |
| Google Analytics | `<head>` に GA4 タグを埋め込み |
| 選手カードの追加 | `players-grid` に `.player-card` を追加し `images/` に画像を配置 |
| 選手詳細モーダル | カードクリックで詳細情報をモーダル表示 |
