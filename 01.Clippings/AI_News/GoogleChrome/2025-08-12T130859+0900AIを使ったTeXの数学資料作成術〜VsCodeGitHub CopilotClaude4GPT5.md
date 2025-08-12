---
title: "AIを使ったTeXの数学資料作成術〜VsCode/GitHub Copilot/Claude4/GPT5"
source: "https://qiita.com/kenjihiranabe/items/4c517037a86d5ae0983c"
author:
  - "[[kenjihiranabe]]"
published: 2025-08-10
created: 2025-08-12
description: "数学の資料づくりに TeX(LaTeX)を利用している人は多いと思います。 プログラマの私がコーディングに使っているVsCode+GitHub Copilot環境を使って、実際に資料を作るデモ動画です。 コードと数学のTeX文章の違い 数学のTeX文章は、「コード」の意..."
tags:
  - "clippings"
---
![](https://relay-dsp.ad-m.asia/dmp/sync/bizmatrix?pid=c3ed207b574cf11376&d=x18o8hduaj&uid=)

## Qiitaにログインして、便利な機能を使ってみませんか？

あなたにマッチした記事をお届けします

便利な情報をあとから読み返せます

[ログイン](https://qiita.com/login?callback_action=login_or_signup&redirect_to=%2Fkenjihiranabe%2Fitems%2F4c517037a86d5ae0983c&realm=qiita) [新規登録](https://qiita.com/signup?callback_action=login_or_signup&redirect_to=%2Fkenjihiranabe%2Fitems%2F4c517037a86d5ae0983c&realm=qiita)

数学の資料づくりに TeX(LaTeX)を利用している人は多いと思います。  
プログラマの私がコーディングに使っているVsCode+GitHub Copilot環境を使って、実際に資料を作るデモ動画です。

![](https://www.youtube.com/watch?v=jyjmfGLAL-w)

## コードと数学のTeX文章の違い

数学のTeX文章は、「コード」の意味と「文章」の両方の意味を持っています。  
文章は書けても、数式のTeXコードはなかなか書き慣れないと書けないのです。特に行列などを書くのは結構大変で、私はネットと調べて「コピペ」を多用していました。また、Goodnotes のような iPad と Apple Pencil で手書きからの変換もためしてみていましたが、やっぱりまどろっこしく感じていました。

ところが、AIの登場によって、コーディングアシスタント、とくに Agent Modeが現れて、このコード部分の補完がとても楽になりました。TeXの文章に苦戦している人がぜひ試して見るべきだ、と思って公開しました。

TeXによる数式を含む文章は、小説のように通常の文章とも違うし、コードとも違います。文章は埋め込まれた書式をもとに美しい数式としてPDFに出すことができます。最終ユーザは文章を直接読みます。「届く文章」を書く力が著者には必要です。

プログラミングでは、最終ユーザはコードを読みません。ユーザインターフェイスを通してそのアプリケーションを利用します。プログラマがコードを書きます、読みやすいコードを書く技術は必須ですが、その「内部品質」はユーザには届きません。

AIでTeX文書を書いていると、この難しい数式のTeX文法での書き方の部分をまるっと、AIにお願いできるんです！TeXでハマると、その調査やデバッグに数時間かかってしまうこともあります。インターネット上にはいろんな参考になるサイトもあるのですが、やはり、文章に専念したい！と思うのです。

もう一つのAIの利点は、数学の知識をLLMが持っているということ。定理の名前などを入れたら、すぐにその周辺の文章は補完してくれます。もちろん著者はそれをそのまま使う、ということは少ないでしょうが、圧倒的な知識を提供してくれます。

3つ目は、「レビュー能力」です。矛盾点や計算の間違いも指摘してくれるという優れもの。「批判的な視点でレビューして」と言うことで、いつも褒めるリアクションをしているLLMも、しっかり矛盾点を突いてきます。もちろんいつも正しいとは限りませんが、多くの場合もっともな指摘です。優秀なレビューアです。

昔は掛け算もできない、と言われていましたが、行列計算できます。ぼくが気づいたのは、行列を与えて、QR分解してください、といったら、TeXで綺麗に途中計算含めてやってくれました。「検算してもとの行列が復元できるかチェックして」を忘れないことです。

## Knuth 先生が作った対称的なTeXとWeave

よく考えて見ると、TeX を作った Knuth 先生が作った文芸的プログラミング言語 Weave がコメントとコードを織りなすように書いていく（コード主体）のとちょうど対称になっている文章版が、TeX なんですね（文章主体。ちょうど、JavaScript と html 埋め込みの関係に見えてきた）。中心が「文章」なのか「コード」なのか。

しかし、Weave を先に作って、それを使って TeX コンパイラを書いた、というのはすごい先見の名というか、恐れ多いですが、「さすがですKnuth先生！」

## ドメイン知識との接続容易性

さらに、杉本さんと twitter で話をしていて、数学は、そのドメインに強烈な知識の蓄えが LLM の学習できる形であるということ。数学の定義や定理は、名前を持って圧縮された「数学ドメイン」の強い語彙なんです。この定理名や定義、を伝えることで、AIはかなり上手に、書き手の知識を補完してくれます。

プログラミングについては、コードは膨大にありますが、そのコードと「ドメイン知識」をつなぐ部分が数学の定理のようにしっかりしていない、場所によって揺れる、毎回発見される、という特性があるんです。デザインパターンのような汎用的なものや、分野別アナリシスパターンなどが求められる領域なんでしょう。

そう考えると、DDDの「ユビキタス言語」コンセプトはとても良い線行っていると思います。それを、現在は、AIの「コンテキスト」という短期記憶に収めないといけない。うまう名前づけされたドメインのパターンが、再利用な形で（AIが読める）扱えるようになるといいのかな。などと思いました。

## エディタ設定

ここに、自分の設定を置いておきます。ポイントは、

- エディタ自身のサジェスト（補完）を切ります。Copilotのサジェストとぶつからないように。
- TeXのレシピには make を使います（latexmkなどでもよい）。
- PDF のビューアは別ウィンドで。

```json
{
    "terminal.integrated.scrollback": 10000,
    // ---------- LaTeX Workshop ----------
    // 使用パッケージのコマンドや環境の補完を有効にする
    "latex-workshop.intellisense.package.enabled": true,
    // 生成ファイルを削除するときに対象とするファイル
    // デフォルト値に "*.synctex.gz" を追加
    "latex-workshop.latex.clean.fileTypes": [
    *.aux","*.bbl","*.blg","*.idx","*.ind","*.lof","*.lot","*.out","*.toc","*.acn","*.acr","*.alg","*.glg","*.glo","*.gls","*.ist","*.fls","*.log","*.fdb_latexmk","*.snm","*.nav","*.dvi","*.synctex.gz"
    ],
    // 中間ファイルの書き出し先
    "latex-workshop.latex.outDir": "out",
    // ファイル保存時に自動でビルドを実行
    "latex-workshop.latex.autoBuild.run": "onSave",
    // ビルド完了時にPDFビューアーを自動で更新
    "latex-workshop.synctex.afterBuild.enabled": true,
    // ビルドのレシピ
    "latex-workshop.latex.recipes": [
        {
            "name": "make",
            "tools": ["make"]
        },
    ],
    // ビルドのレシピに使われるパーツ
    "latex-workshop.latex.tools": [
        {
            "name": "make",
            "command": "make",
            "args": [],
        },
    ],
    // PDFビューアーはメインと別ウィンドで
    "latex-workshop.view.pdf.viewer": "singleton",
    "editor.inlineSuggest.enabled": true,
    // 設定ファイルは機密が含まれる可能性があるため
    "github.copilot.enable": {
        "*": true,
        "plaintext": false,
        "scminput": false,
        "yaml": false,
    },
    "github.copilot.nextEditSuggestions.enabled": true,
    // LaTeXでは補完を無効にする
    "[latex]": {
        "editor.quickSuggestions": {
            "comments": "off",
            "strings": "off",
            "other": "off"
        },
        "editor.suggestOnTriggerCharacters": false,
        "editor.tabCompletion": "off"
    },
    "workbench.editor.enablePreview": false
}
```

[0](https://qiita.com/kenjihiranabe/items/#comments)

コメント一覧へ移動

X（Twitter）でシェアする

Facebookでシェアする

はてなブックマークに追加する

新規登録して、もっと便利にQiitaを使ってみよう

1. あなたにマッチした記事をお届けします
2. 便利な情報をあとで効率的に読み返せます
3. ダークテーマを利用できます
[ログインすると使える機能について](https://help.qiita.com/ja/articles/qiita-login-user)

[新規登録](https://qiita.com/signup?callback_action=login_or_signup&redirect_to=%2Fkenjihiranabe%2Fitems%2F4c517037a86d5ae0983c&realm=qiita) [ログイン](https://qiita.com/login?callback_action=login_or_signup&redirect_to=%2Fkenjihiranabe%2Fitems%2F4c517037a86d5ae0983c&realm=qiita)

[15](https://qiita.com/kenjihiranabe/items/4c517037a86d5ae0983c/likers)

いいねしたユーザー一覧へ移動

15