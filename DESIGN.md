# DESIGN.md — Base Template

> 汎用ベーステンプレート。案件ごとにセクション1・2を差し替えて使用する。
> セクション3以降は「品質の土台」として基本的に固定。

---

## 1. Visual Theme & Atmosphere

<!-- ★ 案件ごとにここを書き換える -->

- **デザイン方針**: （案件に応じて記述。例: クリーン、温かみのある、高級感）
- **密度**: （例: ゆったりとしたLP型 / 情報量の多いサービス型）
- **キーワード**: （3〜5つの形容詞で雰囲気を表現）

---

## 2. Color Palette & Roles

<!-- ★ 案件ごとにここを書き換える。色はすべて hex 値で指定 -->

### Primary（ブランドカラー）

- **Primary** (`#______`): メインのブランドカラー。CTAボタン、リンク等に使用
- **Primary Dark** (`#______`): ホバー・プレス時のプライマリカラー

### Semantic（意味的な色）

- **Danger** (`#DC3545`): エラー、削除、危険な操作
- **Warning** (`#F59E0B`): 警告、注意喚起
- **Success** (`#10B981`): 成功、完了

### Neutral（ニュートラル）

- **Text Primary** (`#1a1a1a`): 本文テキスト（純黒は使わない）
- **Text Secondary** (`#6b7280`): 補足テキスト、ラベル
- **Text Disabled** (`#9ca3af`): 無効状態のテキスト
- **Border** (`#e5e7eb`): 区切り線、入力欄の枠
- **Background** (`#ffffff`): ページ背景
- **Surface** (`#f9fafb`): カード、セクション背景

---

## 3. Typography Rules

### 3.1 和文フォント

- **ゴシック体**: Noto Sans JP, 游ゴシック体, "Yu Gothic", YuGothic, ヒラギノ角ゴ ProN, "Hiragino Kaku Gothic ProN"
- **明朝体**（アクセントに使用する場合）: Noto Serif JP, 游明朝体, "Yu Mincho", YuMincho, ヒラギノ明朝 ProN, "Hiragino Mincho ProN"

### 3.2 欧文フォント

- **サンセリフ**: "Helvetica Neue", Arial
- **セリフ**: Georgia, "Times New Roman"
- **等幅**: SFMono-Regular, Consolas, Menlo

### 3.3 font-family 指定

```css
/* 本文・見出し（ゴシック） */
font-family: "Noto Sans JP", "游ゴシック体", YuGothic, "ヒラギノ角ゴ ProN", "Hiragino Kaku Gothic ProN", "Helvetica Neue", Arial, sans-serif;

/* 明朝体（アクセント用） */
font-family: "Noto Serif JP", "游明朝体", YuMincho, "ヒラギノ明朝 ProN", "Hiragino Mincho ProN", Georgia, serif;

/* 等幅 */
font-family: SFMono-Regular, Consolas, Menlo, monospace;
```

**フォールバックの考え方**:
- Noto Sans JP を最優先（Google Fonts で確実に読み込める）
- OS搭載の和文フォント（游ゴシック → ヒラギノ）で段階的にフォールバック
- 最後に generic family で保険をかける

### 3.4 文字サイズ・ウェイト階層

| Role | Font | Size | Weight | Line Height | Letter Spacing | 備考 |
|------|------|------|--------|-------------|----------------|------|
| Display | ゴシック | 48px | 700 | 1.3 | 0.02em | ヒーロー見出し |
| Heading 1 | ゴシック | 36px | 700 | 1.4 | 0.02em | セクション見出し |
| Heading 2 | ゴシック | 28px | 700 | 1.4 | 0.02em | サブ見出し |
| Heading 3 | ゴシック | 22px | 600 | 1.5 | 0.02em | 小見出し |
| Body | ゴシック | 16px | 400 | 1.8 | 0.05em | 本文 |
| Caption | ゴシック | 14px | 400 | 1.7 | 0.04em | 補足、注釈 |
| Small | ゴシック | 12px | 400 | 1.6 | 0.04em | 最小テキスト |

### 3.5 行間・字間

- **本文の行間 (line-height)**: 1.8（日本語の可読性を重視）
- **見出しの行間**: 1.3〜1.4
- **本文の字間 (letter-spacing)**: 0.05em
- **見出しの字間**: 0.02em

**ガイドライン**:
- 日本語本文は `line-height: 1.8` を基本とする
- `letter-spacing: 0.05em` で全角文字の詰まりを緩和
- 欧文が混じる場合もこの設定で自然に見える範囲に収まる

### 3.6 禁則処理・改行ルール

```css
word-break: break-all;
overflow-wrap: break-word;
line-break: strict;
```

**禁則対象**:
- 行頭禁止: `）」』】〕〉》」】、。，．・：；？！`
- 行末禁止: `（「『【〔〈《「【`

### 3.7 OpenType 機能

```css
/* 見出し・ナビゲーション */
font-feature-settings: "palt" 1, "kern" 1;

/* 本文 — paltは適用しない（可読性優先） */
font-feature-settings: "kern" 1;
```

### 3.8 縦書き

該当なし（必要な案件では個別に設定）

---

## 4. Component Stylings

### Buttons

**Primary**
- Background: var(--color-primary)
- Text: `#ffffff`
- Padding: 14px 32px
- Border Radius: 8px
- Font Size: 16px
- Font Weight: 600
- Transition: background-color 0.2s ease

**Secondary**
- Background: `transparent`
- Text: var(--color-primary)
- Border: 2px solid var(--color-primary)
- Padding: 14px 32px
- Border Radius: 8px

### Inputs

- Background: `#ffffff`
- Border: 1px solid `#e5e7eb`
- Border (focus): 2px solid var(--color-primary)
- Border Radius: 8px
- Padding: 12px 16px
- Font Size: 16px（モバイルでのズーム防止のため16px以上）
- Height: 48px

### Cards

- Background: `#ffffff`
- Border: 1px solid `#e5e7eb`
- Border Radius: 12px
- Padding: 24px
- Shadow: Level 1（下記参照）

---

## 5. Layout Principles

### Spacing Scale（8px基準）

| Token | Value |
|-------|-------|
| XS | 8px |
| S | 16px |
| M | 24px |
| L | 32px |
| XL | 48px |
| XXL | 64px |
| Section | 120px |

### Container

- Max Width: 1200px
- Padding (horizontal): 24px（モバイル: 16px）

### Grid

- Columns: 12
- Gutter: 24px（モバイル: 16px）

### セクション間の余白

- セクション間: 120px 以上
- セクション内のブロック間: 48px〜64px
- 要素間: 意味的なグループ単位で16px〜24px

---

## 6. Depth & Elevation

| Level | Shadow | 用途 |
|-------|--------|------|
| 0 | none | フラットな要素 |
| 1 | `0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06)` | カード、ドロップダウン |
| 2 | `0 4px 12px rgba(0,0,0,0.1)` | ホバー状態のカード、ポップオーバー |
| 3 | `0 12px 32px rgba(0,0,0,0.12)` | モーダル、ダイアログ |

---

## 7. Do's and Don'ts

### Do（推奨）

- フォントは必ずフォールバックチェーンを指定する
- 日本語本文の line-height は 1.8 にする
- 色のコントラスト比は WCAG AA 以上を確保する
- 余白は Spacing Scale（8px刻み）に従う
- ヒーローカラー1色 + ニュートラル + アクセント1色の3色構成にする
- アニメーションは IntersectionObserver + CSS transition で実装する
- 画像は WebP 想定。alt テキスト必須
- モバイルファーストで実装する

### Don't（禁止）

- `font-family` に和文フォント1つだけを指定しない
- 日本語本文に `line-height: 1.5` 未満を使わない
- 全角・半角スペースを混在させない
- テキストの色に純粋な `#000000` を使わない
- 5色均等の配色にしない（3色構成を守る）
- Bootstrap / Tailwind CDN を無断で導入しない
- 装飾目的のみのグラデーション多重使用をしない
- 同一ブロック内で3種類以上のアニメーションを使わない

---

## 8. Responsive Behavior

### Breakpoints

| Name | Width | 説明 |
|------|-------|------|
| Mobile | ≤ 767px | モバイルレイアウト |
| Tablet | 768px〜1199px | タブレットレイアウト |
| Desktop | ≥ 1200px | デスクトップレイアウト |

### タッチターゲット

- 最小サイズ: 44px × 44px（WCAG基準）

### フォントサイズの調整

- モバイル: 本文 15px、Display 28px、H1 24px
- タブレット: 本文 16px、Display 36px、H1 30px
- デスクトップ: 本文 16px、Display 48px、H1 36px

---

## 9. Agent Prompt Guide

### クイックリファレンス

```
Text Color: #1a1a1a
Background: #ffffff
Font: "Noto Sans JP", "游ゴシック体", YuGothic, "ヒラギノ角ゴ ProN", sans-serif
Body Size: 16px
Line Height: 1.8
Letter Spacing: 0.05em
Spacing Unit: 8px
Breakpoints: 768px / 1200px
```

### 使い方

1. このファイルをプロジェクトルートに `DESIGN.md` として配置
2. セクション1（Visual Theme）に案件の雰囲気を記述
3. セクション2（Color Palette）に案件のブランドカラーを記入
4. セクション3〜9はそのまま使用（品質の土台）
