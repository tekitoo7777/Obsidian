---
marp: true
# ↓↓↓ これらの行はテンプレートが機能するために必要です ↓↓↓
header: ' '
footer: ' '
---

<style>
/* Google Fontsから日本語フォントを読み込み */
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700&display=swap');

/* --- 色やフォントの基本設定 --- */
:root {
  --color-background: #f8f8f4;
  --color-foreground: #3a3b5a;
  --color-heading: #4f86c6;
  --color-hr: #000000;
  --font-default: 'Noto Sans JP', 'Hiragino Kaku Gothic ProN', 'Meiryo', sans-serif;
}

/* --- スライド全体のスタイル --- */
section {
  background-color: var(--color-background);
  color: var(--color-foreground);
  font-family: var(--font-default);
  font-weight: 400;
  box-sizing: border-box;
  border-bottom: 8px solid var(--color-hr);
  position: relative;
  line-height: 1.7;
  font-size: 22px;
  padding: 56px;
}
section:last-of-type {
  border-bottom: none;
}

/* --- 見出しのスタイル --- */
h1, h2, h3, h4, h5, h6 {
  font-weight: 700;
  color: var(--color-heading);
  margin: 0;
  padding: 0;
}

/* タイトルページ(h1)のスタイル */
h1 {
  font-size: 56px;
  line-height: 1.4;
  text-align: left;
}

/* 通常スライドのタイトル(##) */
h2 {
  position: absolute;
  top: 40px;
  left: 56px;
  right: 56px;
  font-size: 40px;
  padding-top: 0;
  padding-bottom: 16px;
}

/* h2の疑似要素(::after)を使って、短い線を実装 */
h2::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 8px;
  width: 60px;
  height: 2px;
  background-color: var(--color-hr);
}

/* h2と後続コンテンツの間のスペースを確保 */
h2 + * {
  margin-top: 112px;
}

/* サブ見出し (例: 目的, 目標) */
h3 {
  color: var(--color-foreground);
  font-size: 28px;
  margin-top: 32px;
  margin-bottom: 12px;
}

/* --- リストのスタイル --- */
ul, ol {
  padding-left: 32px;
}
li {
  margin-bottom: 10px;
}

/* フッターとして機能する、太い青いラインを実装 */
footer {
  font-size: 0;
  color: transparent;
  position: absolute;
  left: 56px;
  right: 56px;
  bottom: 40px;
  height: 8px;
  background-color: var(--color-heading);
}

/* ★★★ ロゴの配置方法を、calc()を使った最も堅牢な方法に変更 ★★★ */
header {
  font-size: 0;
  color: transparent;
  background-image: url('ロゴ.png');
  background-repeat: no-repeat;
  background-size: contain;
  background-position: top right;
  
  position: absolute;
  top: 40px;
  
  /* rightプロパティの代わりに、calc()で左からの位置を計算して配置を安定させます */
  /* 計算式: (コンテナの幅 - ロゴの幅 - 右の余白) */
  left: calc(100% - 180px - 56px);
  
  /*
    【重要】下のwidthの値を変更した場合、
    上のcalc()内の「180px」も同じ値にしてください。
  */
  width: 180px;
  height: 50px;
}

/* --- 特別なクラス --- */
section.lead {
  border-bottom: 8px solid var(--color-hr);
}

/* タイトルページではフッターラインとロゴ(header)を非表示にする */
section.lead footer,
section.lead header {
  display: none;
}

section.lead h1 {
  margin-bottom: 24px;
}
section.lead p {
  font-size: 24px;
  color: var(--color-foreground);
}

/* ガイドライン用のスタイル */
.bad-example {
  background-color: #fbe9e7;
  color: #c62828;
  padding: 8px 16px;
  border-radius: 4px;
}
</style>

# Cursor勉強会
# 教育関係者のためのAI駆動開発入門

**テキトー教師**  
*2025年8月*

---

## 今日の内容

1. **Cursorとは？** - AI搭載エディタの基本
2. **インストールと設定** - 始め方ガイド
3. **おすすめプラグイン** - 便利な機能
4. **実践例** - 
5. **まとめ** - 

---

## Cursorとは？

### AI搭載の次世代コードエディタ

- **開発元**: Anysphere（エニスフィア）
- **価格**: 学生は1年間**無料**
- **対応OS**: Windows, macOS, Linux

---

## Cursorでできること

- **チャット機能**: コードについて質問ができる機能  
- **エージェント機能**: タスク自動化・コマンド実行
- **ルール機能**: AIの動作を定義するカスタム命令
- **MCP**: Notion、Slackなどと連携  

---

## 料金プラン

### 無料プラン
- GPT-3.5を月200回まで利用可能
- GPT-4を月50回まで利用可能

### Proプラン（$20/月）
- GPT-4を月500回まで高速利用
- 優先サポートあり

---

## 教育現場での活用メリット

✅ **プログラミング未経験でも始められる**  
✅ **教材作成の効率化が可能**  
✅ **業務自動化を実現**  
✅ **個人のQOLアップ**  
✅ **インプット・アウトプットの向上**

---

## インストール手順

### 1. ダウンロード

1. [Cursor公式サイト](https://cursor.com/ja/students)にアクセス
2. 「Download for free」をクリック
3. OSに応じたインストーラーをダウンロード

---

## 初回セットアップ

### アカウント作成
- メールアドレスでサインアップ

### 日本語設定
- `Ctrl/Cmd + Shift + P`でコマンドパレット
- "Configure Display Language"を検索
- "ja"を選択して日本語に変更

---

## テーマ設定

### 推奨設定
- `Ctrl/Cmd + ,`で設定を開く
- ワークベンチ→外観→"Color Theme"
- **教育現場では「Light」テーマがおすすめ**

---

## 基本的な画面構成

![Cursor画面構成](./images/CleanShot%202025-08-07%20at%2012.06.54@2x.png)

---

## おすすめプラグイン

### 便利なプラグイン
- **Gemini Code Assist**: AIによるコード補完
- **Claude Code**: AIによるコード生成・修正
- **Japanese Language Pack**: 日本語化

---

## プラグインのインストール

### インストール手順

1. `Ctrl/Cmd + Shift + X`で拡張機能を開く
2. プラグイン名を検索
3. 「Install」をクリック
4. 必要に応じて再起動

---

## Cursorで何ができる？

### 実践例を紹介します

実際に作成した3つのアプリケーション事例を
順番にご紹介いたします

---

## 実践例1：デスクトップ整理

### 課題
デスクトップがファイルで溢れかえっている

### 解決策
- ファイルを自動で分類・整理
- 定期的な整理の自動化
- ファイル検索機能の実装

---

## 実践例1：参考記事

**参考記事**: [学校の先生必見！Cursorを使って
デスクトップを整理してもらおうとしたら、
自動整理システムまで作ってくれた話](https://note.com/tekitooooo/n/nd509d070da93)

---

## 実践例2：教育アプリ開発

### 課題
教育現場で使えるアプリを作りたい

### 解決策
- 提出物管理アプリ
- 教育ニュース自動投稿システム
- 数学教材の可視化

---

## 実践例2：参考記事

**参考記事**: [【実践報告】CursorとClaudeで
教育アプリ、教材を開発してみた！
ノンプログラマー教員でも作れる3つの事例](https://note.com/tekitooooo/n/n0ea56578cdd2)

---

## 実践例3：QOLアップ

### 課題
日々の振り返りとインプット・アウトプットの
質と量を向上させたい

### 解決策
- ファイル管理の自動化
- 文章生成の効率化
- 日記管理のシステム化

---

## まとめ

### Cursorで実現できること
- **プログラミング学習の効率化**
- **教材作成の自動化**
- **業務プロセスの改善**
- **個人の生産性向上**

---

## お問い合わせ

**テキトー教師**
- Twitter: [@tekitoo_t_cher](https://mobile.twitter.com/tekitoo_t_cher)
- Note: [tekitooooo](https://note.com/tekitooooo)
- Discord: [AIを使ってゆとりを取り戻す！](https://discord.gg/WtvrgkU8)

**ご質問・ご相談お待ちしています！**
