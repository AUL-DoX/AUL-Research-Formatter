# AUL Research Formatter

**非構造テキスト → 構造テキスト変換ツール**

Gemini Deep Research などのAIリサーチ出力（改行なし・表崩れ）を、Markdown / HTML / note / Google Docs 形式に自動変換するスタンドアロンHTMLツール。

---

## Demo

```
入力（Gemini Deep Research コピペ）
──────────────────────────────────
現代日本における労働需給の構造的再考：マクロ統計上の「人手不足」と「ミッシングワーカー」の重層的分析労働需給のパラドックス：過去最高の労働供給と深刻な不足感の共存現代日本の労働市場は…指標名数値・現状備考出典全国労働力人口6,957万人2024年平均…

↓ 変換

出力（Markdown）
──────────────────────────────────
# 現代日本における労働需給の構造的再考

## 労働需給のパラドックス：過去最高の労働供給と深刻な不足感の共存

現代日本の労働市場は…

| 指標名 | 数値・現状 | 備考 |
|---|---|---|
| 全国労働力人口 | 6,957万人 | 2024年平均、過去最高 |
…
```

---

## Features

- **見出し検出** — `タイトル：サブタイトル` 形式・記号（■◆▶）・短行パターンから h1/h2/h3 を自動判定
- **段落分割** — 改行なしテキストを句点（。！？）で自然な段落に復元
- **表検出** — パイプ区切り・スペース整形・インライン連結の3パターンに対応
- **箇条書き復元** — `・●○▸①` など多様な記号を統一された Markdown リストに変換
- **4形式出力** — Markdown / HTML / note 用 / Google Docs 用
- **RAW / PREVIEW 切り替え** — 変換結果をその場でプレビュー確認
- **コピー / DL** — ワンクリックでクリップボードコピーまたはファイルダウンロード

---

## Installation

インストール不要。HTMLファイルをダブルクリックするだけ。

```bash
git clone https://github.com/AUL-DoX/aul-research-formatter.git
```

`AUL-Research-Formatter-v2.html` をブラウザで開く。

または [Releases](../../releases) から最新版をダウンロード。

---

## Usage

1. Gemini Deep Research（または任意のAIリサーチツール）の出力テキストをコピー
2. 左ペインに貼り付け
3. 出力形式を選択（Markdown / HTML / note / Google Docs）
4. **変換 →** ボタンをクリック
5. RAW タブでコードを確認、PREVIEW タブでレンダリングを確認
6. **コピー** または **DL** で出力を取得

---

## Output Formats

| 形式 | 用途 | 備考 |
|---|---|---|
| Markdown | ブログ・GitHub・Obsidian など | 標準 CommonMark 準拠 |
| HTML | Webページとしてそのまま使用 | CSSスタイル付き完全HTML |
| note | note.com 記事エディタへ貼り付け | 表は箇条書きに自動変換（note非対応のため） |
| Google Docs | Google ドキュメントへインポート | 「Markdownとして貼り付け」機能対応 |

---

## Supported Input Patterns

| パターン | 例 | 対応状況 |
|---|---|---|
| 改行なし連結テキスト | Gemini コピペ出力 | ✅ 改行復元処理 |
| パイプ区切り表 | `\| 列1 \| 列2 \|` | ✅ |
| スペース/タブ整形表 | インデント＋スペース区切り | ✅ |
| インライン連結表 | `指標名数値備考全国労働力人口…` | ✅ パターンマッチで抽出 |
| 記号付き見出し | `■◆▶【` で始まる行 | ✅ |
| 番号付き見出し | `第1章` `1. タイトル` | ✅ |
| 各種箇条書き | `・●○①1.` など | ✅ |
| 数式（LaTeX） | `$$L_d(w) > L_s(w)$$` | ⚠️ テキストとして出力 |
| 完全崩壊表 | 列境界が不明な1行連結 | ⚠️ 部分対応（API連携で改善予定） |

---

## Architecture

```
AUL-Research-Formatter-v2.html  （単一ファイル）
│
├── CSS           ダークテーマ UI
├── HTML          2ペインレイアウト（入力 / 出力）
└── JavaScript
    ├── restoreLineBreaks()     改行復元（Step 1）
    ├── extractInlineTables()   インライン表抽出（Step 2）
    ├── parse()                 ブロック構造解析
    ├── render()                形式別レンダリング
    └── helpers
        ├── isSpaceTableLine()  スペース表判定
        ├── spaceTableToPipe()  スペース表→パイプ変換
        ├── normTable()         テーブル正規化
        └── md2html()           プレビュー用MDレンダリング
```

---

## Requirements

- モダンブラウザ（Chrome / Firefox / Edge / Safari）
- インターネット接続不要
- APIキー不要
- サーバー不要

---

## Privacy

- すべての処理はブラウザ内で完結
- 外部サーバーへのデータ送信なし
- 入力テキストはローカルメモリのみで処理

福祉・医療・教育など情報管理が厳しい現場での利用を想定して設計。

---

## Roadmap

- [ ] Claude API 連携モード（崩壊表の完全復元）
- [ ] Gemini API 連携モード
- [ ] GAS（Google Apps Script）版
- [ ] note.com API 連携（直接投稿）
- [ ] カスタム表ヘッダー辞書の設定

---

## License

MIT License

---

## Author

**AUL-DoX** — 福祉・教育・ケア現場のデジタル化を支援するツール開発

- Website: [aul-dox.jp](https://aul-dox.jp)
- GitHub: [@AUL-DoX](https://github.com/AUL-DoX)
