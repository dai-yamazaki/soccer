2026 FIFAワールドカップの最新試合結果をWebで収集し、results.html のスコアを更新して GitHub Pages に反映する。

## 対象ファイル

```
/Users/daiyamazaki/AI_Projects/21_soccer/02_2026WorldCup/01_time table/results.html
```

スコアは `MATCHES` 配列内の `hs`（ホーム得点）と `as`（アウェー得点）で管理している。
`null` = 未試合、数値 = 確定スコア。

---

## 手順

### Step 1: 最新結果を検索する

以下のクエリで **WebSearch** を実行する（複数クエリを並列で）:

```
2026 FIFA World Cup results today scores all matches
2026 FIFAワールドカップ 試合結果 スコア 最新
```

見つかった URL は **WebFetch** で本文を取得し、試合ごとのスコアを抽出する。
信頼性の高いソース（FIFA公式・ESPN・SBS・BBC・Sofascore 等）を優先する。

結果が曖昧な場合は追加クエリ（グループ名・対戦国名）でピンポイント検索する。

### Step 2: 対象試合を特定する

results.html の `MATCHES` 配列を読み込み、`hs:null, as:null` のまま **日付が過去** のエントリを抽出する。

```javascript
// 対象エントリの例
{ grp:'A', md:1, date:'06-12', time:'4:00', home:'MX', hs:null, as:null, away:'RSA' }
```

日付の比較基準は **日本時間（JST）の今日の日付**。

### Step 3: スコアを更新する

Step 1 で取得したスコアを該当エントリに書き込む。

```javascript
// 更新後の例（メキシコ 2-0 南アフリカ）
{ grp:'A', md:1, date:'06-12', time:'4:00', home:'MX', hs:2, as:0, away:'RSA' }
```

**注意事項:**
- スコアが確認できなかった試合は `null` のまま残す（推測で埋めない）
- 同じ日付・グループ・対戦カードでも複数エントリがある場合はそれぞれ正確に対応させる
- 第3節（md:3）の同時刻2試合は混同しないよう注意

Edit ツールで `hs:null, as:null` → `hs:X, as:Y` を正確に置換する。

### Step 4: 更新内容を確認する

更新したエントリを一覧で出力し、意図したスコアになっているか確認する。

```
更新した試合:
  グループA MD1: 🇲🇽 メキシコ 2-0 南アフリカ 🇿🇦
  グループA MD1: 🇰🇷 韓国 2-1 チェコ 🇨🇿
  ...
```

### Step 5: コミット・プッシュする

```bash
cd /Users/daiyamazaki/AI_Projects/21_soccer && \
git add "02_2026WorldCup/01_time table/results.html" && \
git commit -m "Update WC results $(date '+%Y-%m-%d'): [更新した試合の概要]" && \
git push origin main
```

コミットメッセージの `[更新した試合の概要]` 部分は実際に更新したグループ・節を記載する。
例: `Update WC results 2026-06-13: Group A MD1, Group B MD1, Group D MD1`

### Step 6: 完了報告

以下の形式で報告する:

```
✅ WCリザルト更新完了（YYYY年MM月DD日）

更新した試合（N試合）:
  グループX MD? : 🏳️ チームA X - Y チームB 🏳️
  ...

未確定（スコア取得できず）:
  グループX MD? : チームA vs チームB（理由があれば記載）

🌐 GitHub Pages: https://dai-yamazaki.github.io/soccer/02_2026WorldCup/01_time%20table/results.html
```

---

## 補足: グループステージ 試合日程（日本時間）

| 節 | 期間 |
|----|------|
| MD1 | 6/12(金)〜6/18(木) |
| MD2 | 6/19(金)〜6/24(水) |
| MD3 | 6/25(木)〜6/28(日) |

日本代表（グループF）の試合:
- MD1: 6/15(月) 5:00 オランダ vs 日本
- MD2: 6/21(日) 13:00 チュニジア vs 日本
- MD3: 6/26(金) 8:00 日本 vs スウェーデン
