# AUL Research Formatter

**非構造テキスト → 構造テキスト変換ツール**

Gemini Deep Research などのAIリサーチ出力（改行なし・表崩れ）を、Markdown / HTML / note / Google Docs 形式に自動変換するスタンドアロンHTMLツール。

![version](https://img.shields.io/badge/version-3.1-brightgreen)
![license](https://img.shields.io/badge/license-MIT-blue)
![offline](https://img.shields.io/badge/offline-ready-lightgrey)

---

## デモ

```
入力（Gemini Deep Research コピペ・改行なし）
────────────────────────────────────────────
現代日本における労働需給の構造的再考：マクロ統計上の「人手不足」と「ミッシングワーカー」
の重層的分析労働需給のパラドックス：過去最高の労働供給と深刻な不足感の共存…
指標名数値現状備考出典全国労働力人口6,957万人2024年平均過去最高…

↓ 変換（3秒）

出力（Markdown）
────────────────────────────────────────────
# 現代日本における労働需給の構造的再考

## 労働需給のパラドックス：過去最高の労働供給と深刻な不足感の共存

現代日本の労働市場は…

| 指標名 | 数値・現状 | 備考 | 出典 |
| --- | --- | --- | --- |
| 全国労働力人口 | 6,957万人 | 2024年平均、過去最高 | 総務省 |
```

---

## 特徴

- **見出し検出** — `タイトル：サブタイトル`形式・記号（■◆▶【）・短行パターンから h1/h2/h3 を自動判定
- **段落分割** — 改行なしテキストを句点（。！？）で自然な段落に復元
- **表検出** — パイプ区切り・スペース整形・完全フラット連結（Gemini特有）の3パターンに対応
- **箇条書き復元** — `・●○▸①` など多様な記号を統一された Markdown リストに変換
- **4形式出力** — Markdown / HTML / note用 / Google Docs用
- **PREVIEW表示** — 変換結果をその場でレンダリング確認（デフォルト）
- **コピー / DL** — ワンクリックでクリップボードコピーまたはファイルダウンロード
- **オフライン動作** — APIキー不要・インストール不要・外部通信なし

---

## 使い方

1. [Releases](../../releases/latest) から `AUL-Research-Formatter.html` をダウンロード
2. ブラウザで開く（ダブルクリックでOK）
3. 左ペインにAIリサーチ出力を貼り付け
4. 出力形式を選択（Markdown / HTML / note / Google Docs）
5. **変換 →** をクリック
6. PREVIEWで確認 → **コピー** または **DL**

---

## 対応入力パターン

| パターン | 具体例 | 状態 |
| --- | --- | --- |
| 改行なし連結テキスト | Gemini コピペ出力 | ✅ |
| パイプ区切り表 | `\| 列1 \| 列2 \|` | ✅ |
| スペース/タブ整形表 | 半角スペース2個以上で区切られた表 | ✅ |
| 完全フラット連結表 | `指標名数値備考全国労働力人口…` | ✅ |
| 記号付き見出し | `■◆▶【` で始まる行 | ✅ |
| コロン見出し | `タイトル：サブタイトル` | ✅ |
| 番号付きリスト | `1.` `①` `（1）` | ✅ |
| 中黒リスト | `・項目` | ✅ |

---

## 出力形式

| 形式 | 主な用途 |
| --- | --- |
| Markdown | ブログ・GitHub・Obsidian |
| HTML | Webページとしてそのまま使用（DL推奨） |
| note | note.com エディタに直接貼り付け |
| Google Docs | 「Markdownとして貼り付け」機能でインポート |

---

## 開発・ビルド（v3以降）

v3からTypeScript + Viteで開発し、ビルド成果物はシングルHTMLとして出力されます。

```bash
git clone https://github.com/AUL-DoX/aul-research-formatter.git
cd aul-research-formatter
npm install

# 開発
npm run dev

# テスト（24本）
npm test

# ビルド → dist/index.html
npm run build
```

### ディレクトリ構成

```
src/
  parser/
    types.ts          # Block型定義
    preprocessor.ts   # 改行復元・表抽出
    parser.ts         # テキスト → Block[]
  renderer/
    renderers.ts      # 4形式レンダラー
  ui/
    app.css
  main.ts
tests/
  parser.test.ts      # Vitest 24テスト
index.html
```

---

## バージョン履歴

| バージョン | 主な変更 |
| --- | --- |
| v3.1 | PREVIEWデフォルト化・HTMLモードDL誘導・/g正規表現バグ修正 |
| v3.0 | TypeScript全面移植・Vitest導入・Vite+singlefileビルド |
| v2.3 | コロン見出し検出・スペース表対応・完全フラットテーブル対応 |
| v2.0 | スタンドアロンHTML・RAW/PREVIEWトグル・4形式出力 |

過去バージョンは [Releases](../../releases) からダウンロードできます。

---

## ライセンス

MIT License — 自由に使用・改変・再配布できます。

---

*[AUL-DoX](https://aul-dox.jp) | 福祉・教育・ケア現場のデジタル化を支援するツール開発*
