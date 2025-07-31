# ChatGPT - Azure OpenAI 大全 - Speaker Deck

作成日: 2025-05-19 19:26:24

## プロパティ

- タグ: AI, 働き方, microsoft, 記事, 教育, プレゼン, 生成ai, 生産性, タスク管理, 動画, chatgpt, マネジメント
- AIによる要約: このドキュメントは、ChatGPTとAzure OpenAIサービスに関する情報をまとめた資料です。GPTの全体像やMicrosoftとOpenAIの関係、Prompt EngineeringやRAGアーキテクチャ、GPTシステムの運用など、さまざまなトピックが含まれています。
- 日付: 2023-12-16

https://speakerdeck.com/hirosatogamo/chatgpt-azure-openai-da-quan
![image_20250519_192624.png](../assets/image_20250519_192624.png)
## Slide 2
### Slide 2 text
2 WHO AM I ? @hiro_gamo Azure OpenAI Champ 元データサイエンティスト。データ基盤、エンタープライズブロックチェーンサービス 構築など経験し、現在はAI/MLシステム開発の技術支援に従事。 HIROSATO GAMO Microsoft Japan Co., Ltd. Cloud Solution Architect (Data & AI) About me 『ChatGPTによって描かれる未来とAI開発の変遷』webセミナー｜IT勉強会・イベントならTECH PLAY［テックプレイ］ 20230421_DS協会のChatGPTセミナーが凄かった件(大城、正式版、4/23、4/24更新)｜ChatGPT部 Produced by NOB DATA (note.com)## Slide 3
### Slide 3 text
3 Agenda Microsoft と OpenAI 2 Prompt Engineering 3 GPTの全体像 1 ⚫ GPT とは何なのか ～チャットAIを例にした動作イメージ～ ⚫ GPT によって実現されたサービス ⚫ Microsoft の GPT 活用 ⚫ GPTに期待される用途の簡易マッピング ⚫ GPTに関するFAQ ⚫ GPT単体の弱点を理解 ⚫ GPTは嘘をつく？ ～不正確性をカバーするアイディア～ ⚫ 外部情報を取得し文脈として与える考え方 Grounding ⚫ GPTと連携するPluginの拡大 ⚫ GPTで描かれる未来 ⚫ OpenAI とは ⚫ テキストから画像を生成するDALL·Eのデモ ⚫ Microsoft と OpenAI について ⚫ Azure における OpenAI Service の位置づけ ⚫ Azure OpenAI Serviceの概要 • Azure OpenAI でしか提供されない特長 • 提供可能なAIモデル一覧 ⚫ GPT 系モデルの種類と用途 ⚫ Azure OpenAI Studio ChatGPT Playground の良さ ⚫ GPT のパラメータの意味 ⚫ GPT の課金単位「トークン」とは ⚫ コストの概算シミュレートをしてみる ⚫ クォータの考え方 ⚫ Microsoft Entra IDによる認証 ⚫ イベントストリーム表示によるユーザへの 待機ストレス軽減 ⚫ ML 開発の今まで ⚫ ML 開発の新しいパラダイム Prompt Engineering ⚫ Fine tuning と Prompt Engineering との位置づけ ⚫ ユーザサイドのPrompt Engineeringテクニック ⚫ AI が解釈しやすく処理する Prompt Processing ⚫ ユーザの力に依存せず優良なプロンプトに 仕上げるには？(アイディア追加版) ⚫ 例示で精度を高める Few-shot Learning ⚫ 段階的な推論をさせる Chain of Thought ⚫ 思考過程パターンを複数生成する Self Consistency ⚫ GPT 自身に出力の再帰的な修正をさせる Recursively Criticizes and Improves ⚫ Grounding を考えさせ、動的にタスク実行する ReAct ⚫ GPT の開発補助に用いられるライブラリ ⚫ GPT パイプライン設計の重要性とPrompt flowの活用## Slide 4
### Slide 4 text
4 Agenda GPTシステムの運用 5 RAGアーキテクチャ 4 ⚫ エンタープライズサーチのサンプルアーキテクチャ ⚫ ドキュメント検索の2つの選択肢 ⚫ Azure AI Search ベクトル検索対応 ⚫ 【補足】文書のインデックス化とは ⚫ 取得情報をGPTに与える際のトークンの節約 (チャンクとは) ⚫ Azure OpenAI on your data 機能 ⚫ GPTシステムにおけるログの重要性 ⚫ プロンプトログの分析によるGPTシステム継続改善例 ⚫ Prompt injection 対策 ⚫ 自前コンテンツフィルタリングのアイディア ⚫ 個人情報を意識したプロンプト管理 (最も規制が厳しいGDPRを例に) ⚫ AIネイティブなアーキテクチャでの運用へ ⚫ AI の構築済みサービスの活用で管理工数を軽減 ⚫ Azure Machine Learning モデルカタログの活用 ⚫ GPTを活用するシステムの参考アーキテクチャ## Slide 5
### Slide 5 text
5 GPTの全体像## Slide 6
### Slide 6 text
6 GPTとは何なのか ～チャットAIを例にした動作イメージ～ テキスト生成過程 戦国時代の終焉の歴史について 教えてください。 ※説明のため、かなり抽象化した表現をしています。実際の処理とは異なりますので、あくまでイメージとしてご認識ください。## Slide 7
### Slide 7 text
7 GPTとは何なのか ～チャットAIを例にした動作イメージ～ 安土桃山城を築き、天下統一を目指した織田▮… テキスト生成過程 戦国時代の終焉の歴史について 教えてください。 ✓ ‘日本の戦国時代の終焉’を検索しています… ※説明のため、かなり抽象化した表現をしています。実際の処理とは異なりますので、あくまでイメージとしてご認識ください。## Slide 8
### Slide 8 text
8 GPTとは何なのか ～チャットAIを例にした動作イメージ～ 安土桃山城を築き、天下統一を目指した織田▮… テキスト生成過程 戦国時代の終焉の歴史について 教えてください。 ■ 応答を停止して ✓ ‘日本の戦国時代の終焉’を検索しています… AIは逐次、次に入りそうな文字(or単語)を予測し、 確率の高いものを埋めていく ※説明のため、かなり抽象化した表現をしています。実際の処理とは異なりますので、あくまでイメージとしてご認識ください。## Slide 9
### Slide 9 text
9 GPTとは何なのか ～チャットAIを例にした動作イメージ～ 安土桃山城を築き、天下統一を目指した織田▮… テキスト生成過程 戦国時代の終焉の歴史について 教えてください。 ■ 応答を停止して ✓ ‘日本の戦国時代の終焉’を検索しています… AIによる次の文字(or単語)の予測 AIは逐次、次に入りそうな文字(or単語)を予測し、 確率の高いものを埋めていく 学習データ プロンプト 文脈 次は何の単語かな？ ※説明のため、かなり抽象化した表現をしています。実際の処理とは異なりますので、あくまでイメージとしてご認識ください。 GPT## Slide 10
### Slide 10 text
10 GPTとは何なのか ～チャットAIを例にした動作イメージ～ 安土桃山城を築き、天下統一を目指した織田▮… テキスト生成過程 戦国時代の終焉の歴史について 教えてください。 ■ 応答を停止して ✓ ‘日本の戦国時代の終焉’を検索しています… AIによる次の文字(or単語)の予測 0 0.1 0.2 0.3 5.3 22.7 71.3 … … … … 信秀 信忠 信長 次の単語の出現確率(％) AIは逐次、次に入りそうな文字(or単語)を予測し、 確率の高いものを埋めていく 次は何の単語かな？ たぶん信長 ※説明のため、かなり抽象化した表現をしています。実際の処理とは異なりますので、あくまでイメージとしてご認識ください。 事実関係でなく出現確率である点に注意 学習データ プロンプト 文脈 GPT## Slide 11
### Slide 11 text
11 GPT の仕組みを理解するための参考リンク ChatGPT の仕組みを理解する（前編） - ABEJA Tech Blog Transformerにおける相対位置エンコーディングを理解する。 - Qiita ChatGPT の仕組みを理解する（後編） - ABEJA Tech Blog [1706.03762] Attention Is All You Need (arxiv.org) つくりながら学ぶ！PyTorchによる発展ディープラーニング | マイナビブックス (mynavi.jp) O'Reilly Japan - 機械学習エンジニアのためのTransformers (oreilly.co.jp) IT Text 自然言語処理の基礎 | Ohmsha O'Reilly Japan - ゼロから作るDeep Learning ❷ (oreilly.co.jp)## Slide 12
### Slide 12 text
12 GPTによって実現された先駆けのサービス 言語生成を使ったサービスが次々と登場。 Github Copilot GPT-3をベースに大量のプログラムコードを読み込ませた「Codex」モデルを採用。 関数名やコメントから開発対象コードを提案する。 全言語平均でコードの46％を生成できるとの集計結果が出ている。 Bing Chat GPT-4を強化した「Prometheus」モデルを採用。 チャット回答にWeb検索結果を付与し、引用元サイトを表示する アプローチで最新情報を加味した新たなユーザ体験を作り出した。 ChatGPT GPT-3.5にチャットのデータセットを使ったファインチューニングモデルと、強化学習を 組み合わせた。人と遜色ない高度なチャット応答を実現し大規模言語モデルの 世界的な流行の火付け役に。 GPT GitHub Copilot now has a better AI model and new capabilities - The GitHub Blog ChatGPT (openai.com) Bing Chat## Slide 13
### Slide 13 text
文章要約、生成、 ニュアンスや文章量 コントロールが可能 自動でデータ分析し グラフ描画、 要約まで可能 アイデアや内容を 示唆するだけで スライドや アニメーションを 自動生成 メールの文言を 自動生成 カレンダーと連携し タスク生成可能。 過去のチャットから 関連ファイルを検索 今後も機能追加予定 Word Excel PowerPoint Outlook Teams Microsoft 365 appsへのネイティブ統合 Microsoft 365 Copilot## Slide 14
### Slide 14 text
15 Microsoft 365 Copilot の活用イメージを掴むならこの動画 The Future of Work With AI - Microsoft March 2023 Event - YouTube## Slide 15
### Slide 15 text
Power Platform タスクの自動化と AIによる推奨 CRMとERPに搭載の AIアシスタント 自然言語を利用 Power Apps 自然言語から Power FXの計算式作成 画像とFigmaを アプリに変換 Power Automate 自然言語から フロー作成 Power Virtual Agents Conversation Boosters による会話生成 Azure OpenAI Serviceを通して、 GPTモデルをテンプレートとして利用可能 AI Builder## Slide 16
### Slide 16 text
提供形態整理 Dynamics 365 Windows Azure OpenAI Service SaaS IaaS/PaaS 今提供されているツールの更なる効率化、機能付加 ツール外の領域（プラットフォーム横断、ビジネス利用）の 更なる効率化、機能付加 通常業務の生産性向上 for ALL 効果 ソリューション ERP・CRM業務の生産性向上 for 営業・会計・IT管理 ノーコード・RPA・BIの生産性向上 for 市民＋プロ開発者 セキュリティ業務の生産性向上 for CISO・SoC 開発業務の生産性向上 for エンジニア ソリューション 効果 顧客体験の向上 特殊業務の生産性向上 for 事業担当者 独自のシステム・サービス開発へ ChatGPTなどの生成AIを組み込み可## Slide 17
### Slide 17 text
18 GPTに期待される用途の簡易マッピング 厳密 創造的 仕事 生活 英会話アプリ コード生成 要件定義 キャラクター 情報検索 文書添削 スライド作成 QAボット ブログ作成 マーケインサイト提案 スマートスピーカー カーナビ メール作成 カウンセリング 教材作成 1次コンサル## Slide 18
### Slide 18 text
19 GPT導入事例のご紹介 ベネッセ 小学生親子向け自由研究生成AI相談サービスを無償提供 ITmedia NEWS 記事執筆にAI導入 Sansan 契約DXサービス「Contact One」にGPT要約を搭載 SmartHR 「従業員サーベイ」機能にAIを利用した自由記述回答要約機能を公開 楽天生命 対話形式の代理店アシスト機能を生成AIで実現 レコチョク 音楽市場で生成AIを活用開始 ワークスアプリケーションズ AIで経営レベルの意思決定を支援 Moody's AIを活用したリスク分析ソリューションを開発 アドバンスト・メディア AI音声認識AmiVoice®搭載の議事録ソリューションにGPTを活用した要約システムを連携し 取手市のDXを推進 rinna AIキャラクター開発力を強化するためにAzure OpenAI Serviceを導入 弁護士ドットコム 弁護士ドットコム - チャット法律相談 (α版) ライオン ChatGPTを活用した業務効率化のポイントを公開 住信SBIネット銀行 大規模言語モデルを活用した実証実験の開始を発表## Slide 19
### Slide 19 text
20 GPTに関するFAQ 覚えません。GPT単体だと会話内容は揮発性です。覚えさせる(という表現も適切では ないですが)にはサービス提供者がGPTにファインチューニングを施す必要があります。した がって、学習されるかどうかはサービス事業主の意思決定に完全に依存します。 事実関係を把握しているわけではないです。学習においては、モデルがトークンを生成す るパラメータが更新され確率分布が改善されるだけです。確定的にその知識を引き出せ るわけではありません。違う文脈や問いかけにおいては間違える可能性は残ります。 GPT単体は自律性が無いので、素の状態ではいわば指示待ち機能になります。 また、作業の最終責任を負うのも人間です。 人間が持っていた作業の一定の割合が自動化されることが期待されます。 AIは指示が無いと動けません。バックエンドプログラムと組み合わせればあたかもAI＋ バックエンドプログラムが人間のように振る舞えますが、人間と同じく権限が無いと他の システムを触りにいっても拒否されます。 勝手に動き出して暴走するんじゃないの？ 私と会話した内容は全部学習して 覚えてくれるんだよね？ AIが学習したら、 事実関係を把握するんだよね？ 人間の仕事を奪うの？ Answer Answer Answer Answer## Slide 20
### Slide 20 text
21 GPT単体の弱点を理解しておけば外部ツールの連携を含めた対処が可能 文脈から推定しにくい数字などのトークン 正しい答えが決まっていない、 似ているが違いが判別しづらい学習データ 学習データが少ないマイナーな事象 GPT単体の弱点 日本語 文章中の数字、例えば「昨年と比べ売上○○％低下」などは正確な数字と 文脈が紐づかないことがあり精度が落ちることがある。 料理のレシピなど、人によって材料や分量が違うケースなどは正誤が安定しない。 逆に物理法則など普遍的な事象の解説では安定する。 正しい事実関係の出現確率を高めるほどの学習ができておらず間違えやすい。 「1998年の日本プロ野球の2軍について教えて」など。 注意の概要・具体例 GPT-4で多少改善はしたが、言語格差が見られる。一般的にGPTの多くは英語の 文章の方が多く学習されているため日本語より精度が高い。 最適経路計算など 言語生成で実現できないロジック 乗換案内のように、路線図情報や駅間所要時間のデータや確立された解法によって 本来は答えが導かれているものは言語モデルには推定しにくい。 最新情報やドメイン固有情報の記述 GPTには膨大なデータが学習されているが、GPTは最新モデルでも2023年4月のもの。 最新情報を聞かれると不正確な回答に。## Slide 21
### Slide 21 text
22 GPT の Hallucination GPTは確率に基づく言語生成モデルです。 十分な学習データや参考情報を与えなければ、正確な回答はできません。 Azure OpenAI の責任あるAIとしての利用に関するベストプラクティス (microsoft.com) 事実関係を示した外部情報をバックエンドで文脈として付与 (次ページのGrounding) ✓ 計算や最適化など苦手なタスクは別ロジックに任せる(3章にて解説) ✓ 取得情報が十分な領域に用途を限定するなど、 情報不足になるような事実関係を求められるサービス設計をしない ✓ Hallucinationをカバーするアイディア 正しい情報が記載されているドキュメントやサイトを併記するか、 回答を動的生成せず正解コンテンツを直接表示する。 ✓## Slide 22
### Slide 22 text
23 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ チャット内容 バックエンド プログラム GPT Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 23
### Slide 23 text
24 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ チャット内容 チャット内容 バックエンド プログラム チャット内容を クエリへ変換 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 24
### Slide 24 text
25 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ チャット内容 チャット内容 クエリ化結果 バックエンド プログラム チャット内容を クエリへ変換 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 25
### Slide 25 text
26 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ Web検索 bing APIなど チャット内容 バックエンド プログラム クエリ「WBC 2023 優勝国」 チャット内容 クエリ化結果 チャット内容を クエリへ変換 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 26
### Slide 26 text
27 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ Web検索 bing APIなど チャット内容 検索結果 バックエンド プログラム クエリ「WBC 2023 優勝国」 チャット内容 クエリ化結果 チャット内容を クエリへ変換 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 27
### Slide 27 text
28 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ Web検索 bing APIなど チャット内容 クエリ「WBC 2023 優勝国」 検索結果 バックエンド プログラム 質問＋検索結果 ユーザへの 返答作成 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 28
### Slide 28 text
29 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ Web検索 bing APIなど チャット内容 クエリ「WBC 2023 優勝国」 検索結果 バックエンド プログラム 質問＋検索結果 回答 ユーザへの 返答作成 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 29
### Slide 29 text
30 外部情報を取得し文脈として与える考え方 Grounding ※Groundingという言葉には若干曖昧さが残る印象です。もっと狭義・広義な意味で用いられることも多いです。 GPT [2302.02662] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning (arxiv.org) 2023年のWBC優勝国はどこ？ ユーザ Web検索 bing APIなど チャット内容 クエリ「WBC 2023 優勝国」 検索結果 バックエンド プログラム 質問＋検索結果 回答 2023年のWBC優勝国は日本でした。 ユーザへの 返答作成 Groundingを用いることで、Web検索結果や社内データ、外部リソースの計算結果など GPT単体では得られない情報を加味した回答生成が可能。## Slide 30
### Slide 30 text
31 GPT と連携する Plugin の広がり GPT AI Search Azure OpenAI Service Functions Container Appsなど Azure Machine Learning Azure AI Servicesなど 外部サービス 社内に存在するPDF、PowerPoint、Excelファイルなどにおけるテキスト情 報を抽出しておき、GPTのリクエストに応じて検索。質問内容に近い情報 を返答として返す。複数の検索結果の情報を集約し、問いに対するピン ポイントな回答が可能。 社内ナレッジ 検索 あらかじめ用意しておいたプログラムの関数を呼んだり、プロンプトに応じて GPTが生成したコードの実行をすることで様々なタスクが実行可能。 簡単な計算から最適化などの複雑なアルゴリズム、機械の操作なども 視野に入る。 プログラム 実行 構築済みのAIモデルを提供するAPIや、自作の機械学習モデルを呼び出 す。GPTでは処理しにくい自然言語処理タスクをはじめ、 テーブルデータ解析や画像生成、異常検知などを別のAIが解析することで、 GPT単体ではできない高度なタスクまで対応可能。 AI/ML 解析 Web検索や地図情報といった一般的なAPIやサービスを呼ぶことで様々 な機能や手続きが利用可能に。OpenAI社はこの仕組みをPluginと呼 称。例えば社内システムの手続きAPIを準備しておくことでサイトを 移動せずともGPTとの対話で処理を完結させるような応用も。 外部サービス 連携## Slide 31
### Slide 31 text
32 Azure OpenAI Service Plugin (coming soon) Azure AI Search による独自デー タ検索 Azure Translator による 100 を超えるの言語の翻訳 Bing 検索による 最新情報のグラウンディング Azure SQL からの 構造化データの抽出 Azure OpenAI プラグイン • 利用者の様々なデータストア、ベクトル データベース、ウェブ上のデータに安全に アクセスできる • Azure ADとマネージド ID によるデータ アクセス制御 • 管理者ロールはどのプラグインを有効に するか選択可能 OpenAI社、Bing、M365 Copilotなどプラグインプラットフォームを共有した活用が可能に。## Slide 32
### Slide 32 text
33 【補足】AIがサービス利用を仲介する未来像 Pluginによって、デジタルツールがGPTと接続し、人とサービス、サービスとサービスが柔軟に連携可能に ユーザ 情報探索 購買 事務手続き コミュニケーション データ分析 学習 今までの人間とサービスの関係 今までは膨大な数の 各サービス画面で目的を果たしていた。 ログも各サービスが保存。## Slide 33
### Slide 33 text
34 【補足】AIがサービス利用を仲介する未来像 Pluginによって、デジタルツールがGPTと接続し、人とサービス、サービスとサービスが柔軟に連携可能に ユーザ 情報探索 購買 事務手続き コミュニケーション データ分析 学習 ユーザ 情報探索 購買 事務手続き コミュニケーション データ分析 学習 GPT 今までの人間とサービスの関係 AIが人-サービス, サービス-サービスを仲介する世界へ 行動履歴 蓄積 GPTがすべての作業を仲介し、 全ての行動やコミュニケーションを記録しつつ、 適切に過去情報を引き出し支援 GPT GPT## Slide 34
