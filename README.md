# ⚽ 2026 FIFA World Cup 日程管理ツール

2026 FIFA World Cup（米国・カナダ・メキシコ共催）の全試合日程を **日本時間（JST）** で確認できるHTMLツールセット。

🌐 **GitHub Pages で公開中** → https://dai-yamazaki.github.io/soccer/

---

## 📁 ツール一覧

| ツール | 説明 | リンク |
|--------|------|--------|
| 📋 **日程表** | グループA〜L 全72試合をグループ別一覧表示 | [schedule.html](https://dai-yamazaki.github.io/soccer/02_2026WorldCup/01_time%20table/schedule.html) |
| 📅 **カレンダー** | 6月・7月の月間カレンダーで試合日を視覚表示 | [calendar.html](https://dai-yamazaki.github.io/soccer/02_2026WorldCup/01_time%20table/calendar.html) |
| 🏆 **トーナメント表** | ラウンド32〜決勝のブラケット（対戦カード・時刻付き） | [bracket.html](https://dai-yamazaki.github.io/soccer/02_2026WorldCup/01_time%20table/bracket.html) |
| 📖 **マニュアル** | 各ツールの機能説明・データ仕様 | [manual.html](https://dai-yamazaki.github.io/soccer/02_2026WorldCup/01_time%20table/manual.html) |

---

## 🗓️ 大会概要

| 項目 | 内容 |
|------|------|
| 開催期間 | 2026年6月12日(金) 〜 7月20日(月)（日本時間） |
| 開催国 | アメリカ・カナダ・メキシコ（16都市） |
| 出場チーム | 48チーム（グループA〜L、各4チーム） |
| 総試合数 | 104試合（グループ72 ＋ ノックアウト32） |
| 🇯🇵 日本代表 | グループF（オランダ・スウェーデン・チュニジアと同組） |
| 決勝 | MetLife Stadium（ニュージャージー）7/20 4:00 JST |

---

## 🇯🇵 日本代表 試合日程

| 節 | 日本時間 | 対戦 | 会場 |
|----|----------|------|------|
| MD1 | 6/15(月) 5:00 | 🇳🇱 オランダ vs 🇯🇵 **日本** | ダラス |
| MD2 | 6/21(日) 13:00 | 🇹🇳 チュニジア vs 🇯🇵 **日本** | グアダラハラ |
| MD3 | 6/26(金) 8:00 | 🇯🇵 **日本** vs 🇸🇪 スウェーデン | ダラス |

---

## ✨ 主な機能

### 📋 日程表
- グループ別カード（A〜L）で全72試合を整理
- 各チームに国旗絵文字を自動表示
- 日本代表戦の行をハイライト
- ノックアウトステージの日程概要

### 📅 カレンダー
- 月間グリッドで試合日をひと目確認
- グループごとに12色のカラーコーディング
- 🇯🇵 日本戦 → **赤い ★** でマーク
- 注目6か国（🏴󠁧󠁢󠁥󠁮󠁧󠁿🇪🇸🇫🇷🇧🇷🇦🇷🇵🇹）→ **金色の ★** でマーク
- ノックアウトステージをカラーバナーで表示
- ホバーで対戦カード詳細を表示

### 🏆 トーナメント表
- SVGコネクター線付きブラケット
- 全16試合（M73〜M88）のグループ順位ラベルと日本時間を表示
- 日本の進出先スロットに 🇯🇵 マーク
- 3位決定戦・決勝を別枠カードで表示

---

## 🕐 時刻について

全試合時刻は **日本標準時（JST / UTC+9）** に変換して表示。

```
ET（EDT, UTC-4）  + 13時間 = JST
CT（CDT, UTC-5）  + 14時間 = JST
PT（PDT, UTC-7）  + 16時間 = JST
メキシコ（CST, UTC-6）+ 15時間 = JST  ※メキシコはサマータイム廃止済み
```

---

## 📂 リポジトリ構成

```
soccer/
├── index.html                        # GitHub Pages エントリーポイント
├── .nojekyll                         # Jekyll 無効化
├── 02_2026WorldCup/
│   ├── 01_time table/                # ← 日程管理ツール
│   │   ├── schedule.html             #   日程表
│   │   ├── calendar.html             #   カレンダー
│   │   ├── bracket.html              #   トーナメント表
│   │   └── manual.html               #   マニュアル
│   └── 02_LP/                        # ランディングページ素材
└── 01_Arsenal/                       # アーセナル関連
```

---

## 📚 データソース

- 試合日程：[ESPN](https://www.espn.com/soccer/story/_/id/48939282/2026-fifa-world-cup-fixtures-results-match-schedule-group-stage-knockout-rounds-bracket) / [Goal.com 日本](https://www.goal.com/jp/) / [JFA公式](https://www.jfa.jp/samuraiblue/worldcup_2026/schedule_result/)
- ノックアウトステージ対戦カード：[Wikipedia](https://en.wikipedia.org/wiki/2026_FIFA_World_Cup_knockout_stage) / [FIFA公式](https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026/scores-fixtures)

> ⚠️ 試合時刻・対戦カードは公開情報をもとに作成しています。最新情報は[FIFA公式サイト](https://www.fifa.com/ja/tournaments/mens/worldcup/canadamexicousa2026/scores-fixtures)でご確認ください。
