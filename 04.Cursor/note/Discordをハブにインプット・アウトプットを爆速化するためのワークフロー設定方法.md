---
tags:
  - "#AI"
  - "#教育"
  - "#Discord"
  - "#n8n"
  - "#Dify"
  - "#Obsidian"
  - "#自動化"
  - "#ワークフロー設定"
  - "#チュートリアル"
  - "#初心者向け"
  - "#productivity-tools"
published: 2025-01-30
---

# 【完全ガイド】Discordをハブにインプット・アウトプットを爆速化するワークフロー設定方法

## プログラミング初心者でも2時間で構築できる！Discord × n8n × Dify システム

![システム全体像](画像を挿入予定)

こんにちは！テキトー教師です。

今回は、前回の記事「[Discordをハブにインプット・アウトプットを爆速化〜Dify×n8n×Discordボットシステム〜](./Discordをハブにインプット・アウトプットを爆速化〜Dify×n8n×Discordボットシステム〜.md)」で紹介したシステムを、実際にどう構築するか**完全初心者向け**に詳しく解説します。

**この記事の特徴：**
- ✅ 実際に動作するコードとファイルに基づいた解説
- ✅ コピペで使える設定内容
- ✅ つまずきポイントとその解決法


---

## 🎯 完成イメージ：たった2つのリアクションで実現

![完成イメージ](動画を挿入予定)

**構築後にできること：**
- 📝リアクション → Discordメッセージを自動でObsidianに保存
- 🐤リアクション → AIが最適なX投稿文を自動生成してチャンネルに投稿

それでは、実際の設定手順を見ていきましょう！

---

## 📋 事前準備：必要なアカウント（すべて無料）

設定を始める前に、以下のアカウントを準備してください：

### 必須アカウント
- [ ] **Discordアカウント** - メインプラットフォーム
- [ ] **GitHubアカウント** - Obsidianファイル保存用
- [ ] **n8nアカウント** - ワークフロー自動化
- [ ] **Difyアカウント** - AI投稿文生成
- [ ] **Railway/Renderアカウント** - Discord Bot無料ホスティング

### 取得が必要なAPIキー
- [ ] **OpenAI API Key**（月$5程度の従量課金）
- [ ] **GitHub Personal Access Token**（無料）

**💰 料金について：**
ほぼすべて無料プランで運用可能。OpenAI APIのみ使用量に応じた課金（月数百円程度）

---

## 🤖 STEP 1: Discord Botの作成と設定（30分）

### 1-1. Discord Developer Portalでアプリケーション作成

![Discord Developer Portal](画像を挿入予定)

1. **[Discord Developer Portal](https://discord.com/developers/applications)にアクセス**
2. **「New Application」をクリック**
3. **アプリケーション名を入力**
   ```
   例：My Automation Bot
   ```
4. **「Create」をクリック**

### 1-2. Botの設定とトークン取得

![Bot設定画面](画像を挿入予定)

1. **左メニューから「Bot」を選択**
2. **「Reset Token」をクリック**
   ```
   ⚠️ 重要：このトークンは二度と表示されません！
   必ずメモ帳にコピーして保存してください
   ```
3. **「Privileged Gateway Intents」をすべてON**
   - ✅ PRESENCE INTENT
   - ✅ SERVER MEMBERS INTENT  
   - ✅ MESSAGE CONTENT INTENT

### 1-3. Botをサーバーに招待

1. **「OAuth2」→「URL Generator」を選択**
2. **SCOPES選択:**
   - ✅ bot
   - ✅ applications.commands
3. **BOT PERMISSIONS選択:**
   - ✅ Send Messages
   - ✅ Read Messages/View Channels
   - ✅ Read Message History
   - ✅ Add Reactions
4. **生成されたURLでBotを招待**

---

## ⚙️ STEP 2: Discord Botコードの準備（15分）

### 2-1. Botコードの取得

実際に動作しているBotのコードを使用します：

#### `package.json`
```json
{
  "name": "discord-n8n-bot",
  "version": "1.0.0",
  "description": "Discord bot that sends reaction events to n8n webhook",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "axios": "^1.6.5",
    "discord.js": "^14.14.1",
    "dotenv": "^17.2.1",
    "express": "^5.1.0"
  },
  "engines": {
    "node": ">=16.0.0"
  }
}
```

#### `index.js`（メインのBotコード）
```javascript
require('dotenv').config();

const { Client, GatewayIntentBits } = require('discord.js');
const axios = require('axios');
const express = require('express');

// Discord クライアントの初期化
const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.GuildMessageReactions,
    GatewayIntentBits.MessageContent
  ]
});

// 環境変数からWebhook URLを取得
const N8N_WEBHOOK_URL = process.env.N8N_WEBHOOK_URL;
const N8N_X_POST_WEBHOOK_URL = process.env.N8N_X_POST_WEBHOOK_URL;

// Bot起動時の処理
client.once('ready', () => {
  console.log(`Logged in as ${client.user.tag}!`);
});

// リアクション追加時の処理
client.on('messageReactionAdd', async (reaction, user) => {
  if (user.bot) return;
  if (reaction.partial) await reaction.fetch();
  if (reaction.message.partial) await reaction.message.fetch();
  
  const message = reaction.message;
  const emoji = reaction.emoji.name;

  // 📝 リアクション：Obsidian保存用
  if (emoji === '📝' && N8N_WEBHOOK_URL) {
    try {
      const webhookData = {
        event: 'MESSAGE_REACTION_ADD',
        data: {
          messageId: message.id,
          channelId: message.channel.id,
          guildId: message.guild?.id,
          userId: user.id,
          username: user.username,
          content: message.content,
          authorId: message.author.id,
          authorUsername: message.author.username,
          timestamp: message.createdTimestamp,
          emoji: emoji,
          messageUrl: message.url
        }
      };
      await axios.post(N8N_WEBHOOK_URL, webhookData);
      await message.react('✅');
    } catch (error) {
      console.error('Error sending webhook for 📝:', error.message);
      await message.react('❌');
    }
  } 
  // 🐤 リアクション：X投稿文生成用
  else if (emoji === '🐤' && N8N_X_POST_WEBHOOK_URL) {
    try {
      await axios.post(N8N_X_POST_WEBHOOK_URL, {
        event: 'X_POST_REQUEST',
        data: {
          messageId: message.id,
          channelId: message.channel.id,
          content: message.content,
          authorUsername: message.author.username
        }
      });
    } catch (error) {
      console.error('Error sending webhook for 🐤:', error.message);
      await message.channel.send(`❌ n8nワークフローの呼び出しに失敗しました: ${error.message}`);
    }
  }
});

// Express サーバー（n8nからの返信受信用）
const app = express();
app.use(express.json());

// n8nから整形後の投稿文を受け取る
app.post('/draft-post', async (req, res) => {
  const { channelId, draftContent } = req.body;
  if (!channelId || !draftContent) return res.sendStatus(400);

  try {
    const channel = await client.channels.fetch(channelId);
    
    // 生成された投稿文をコードブロックで送信
    await channel.send(`\`\`\`\n${draftContent}\n\`\`\``);
    
    res.sendStatus(200);
  } catch (error) {
    console.error('Error sending final message:', error);
    res.sendStatus(500);
  }
});

// サーバー起動
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`HTTP server listening on port ${PORT}`));

client.login(process.env.DISCORD_BOT_TOKEN);
```

#### `.env`（環境変数ファイル）
```bash
# Discord Bot Token（先ほど取得したトークン）
DISCORD_BOT_TOKEN=your_discord_bot_token_here

# n8n Webhook URLs（後で設定）
N8N_WEBHOOK_URL=https://your-n8n-instance.app/webhook-test/discord-reaction
N8N_X_POST_WEBHOOK_URL=https://your-n8n-instance.app/webhook/x-post

# 環境設定
NODE_ENV=production
```

---

## 🚀 STEP 3: Railway無料ホスティング設定（15分）

### 3-1. Railwayアカウント作成

![Railway設定画面](画像を挿入予定)

1. **[Railway.app](https://railway.app)でアカウント作成**
2. **GitHubアカウントでログイン**
3. **「New Project」をクリック**
4. **「Empty Project」を選択**

### 3-2. プロジェクトのデプロイ

1. **「GitHub Repo」を選択**
2. **Botコードをアップロードしたリポジトリを選択**
3. **自動デプロイが開始される**

### 3-3. 環境変数の設定

1. **プロジェクトの「Variables」タブを開く**
2. **以下を設定：**
   ```
   DISCORD_BOT_TOKEN = 先ほど取得したトークン
   NODE_ENV = production
   ```
3. **「N8N_WEBHOOK_URL」は後でn8n設定後に追加**

---

## 🔧 STEP 4: n8nワークフロー設定（45分）

### 4-1. n8nアカウント作成

![n8n初期画面](画像を挿入予定)

1. **[n8n.io](https://n8n.io)で無料アカウント作成**
2. **「Create Workflow」をクリック**

### 4-2. Obsidian保存ワークフローの構築

このワークフローは📝リアクションでDiscordメッセージをObsidianに保存します。

![Obsidianワークフロー](画像を挿入予定)

#### ワークフロー名：`リアクションDiscord→Obsidian`

**ノード構成：**

1. **Webhook（トリガー）**
   ```json
   設定：
   - HTTP Method: POST
   - Path: /discord-reaction
   ```

2. **Code（データ整形）**
   ```javascript
   // Discordからのデータを取得
   const eventData = $input.item.json.body;

   // 日付フォーマット
   const date = new Date(eventData.data.timestamp);
   const jstDate = new Date(date.getTime() + 9 * 60 * 60 * 1000);
   const dateStr = jstDate.toISOString().split('T')[0];
   const timeStr = jstDate.toTimeString().split(' ')[0];

   // メッセージ内容を取得
   let messageContent = eventData.data.content || "";

   // Obsidianのノート内容を作成
   const noteContent = `# Discord メッセージ

   ## メタデータ
   - **日付**: ${dateStr} ${timeStr}
   - **投稿者**: ${eventData.data.authorUsername}
   - **チャンネルID**: ${eventData.data.channelId}

   ## 内容

   ${messageContent}

   ---
   *📝 リアクションから自動作成*
   `;

   // ファイル名の生成
   const fileName = `Discord_${dateStr}_${eventData.data.messageId}.md`;

   // Base64エンコード
   const contentBase64 = Buffer.from(noteContent).toString('base64');

   return {
     json: {
       fileName: fileName,
       content: noteContent,
       contentBase64: contentBase64,
       channelId: eventData.data.channelId,
       githubApiUrl: `https://api.github.com/repos/YOUR_USERNAME/Obsidian/contents/01.Clippings/Discord/${fileName}`,
       commitMessage: `Discord: ${fileName} を追加`
     }
   };
   ```

3. **Switch（チャンネル別振り分け）**
   ```json
   設定：
   - 条件1: channelId = "VoiceMemoチャンネルID" → voicememo
   - 条件2: channelId = "AIニュースチャンネルID" → ainews  
   - 条件3: channelId = "議事録チャンネルID" → gijiroku
   ```

4. **HTTP Request（GitHub API）**
   ```json
   設定：
   - Method: PUT
   - URL: {{ $json.githubApiUrl }}
   - Authentication: GitHub API
   - Body:
   {
     "message": "{{ $json.commitMessage }}",
     "content": "{{ $json.contentBase64 }}",
     "branch": "main"
   }
   ```

### 4-3. X投稿文生成ワークフローの構築

このワークフローは🐤リアクションでAI投稿文を生成します。

![X投稿ワークフロー](画像を挿入予定)

#### ワークフロー名：`Discord→X`

**ノード構成：**

1. **Webhook（トリガー）**
   ```json
   設定：
   - HTTP Method: POST
   - Path: x-post
   ```

2. **Code（URL判定）**
   ```javascript
   // メッセージ内容を取得
   const messageContent = $input.item.json.body.data.content;

   // URLを検出する正規表現
   const urlRegex = /(https?:\/\/[^\s]+)/g;
   const hasUrl = urlRegex.test(messageContent);

   // 結果をデータに追加
   const item = $input.item;
   item.json.body.data.hasUrl = hasUrl;

   if (hasUrl) {
     item.json.body.data.url = messageContent.match(urlRegex)[0];
     item.json.body.data.user_comment = messageContent.replace(urlRegex, '').trim();
   } else {
     item.json.body.data.url = null;
     item.json.body.data.user_comment = null;
   }

   return item;
   ```

3. **IF（条件分岐）**
   ```json
   設定：
   - 条件: {{ $json.body.data.hasUrl }} is true
   ```

4. **HTTP Request（URL記事処理）**
   ```json
   設定：
   - Method: POST
   - URL: https://api.dify.ai/v1/workflows/run
   - Authentication: Header Auth
   - Headers: Authorization = Bearer YOUR_DIFY_API_KEY
   - Body:
   {
     "inputs": {
       "news_url": "{{ $json.body.data.url }}",
       "user_comment": "{{ $json.body.data.content }}"
     },
     "user": "n8n-workflow"
   }
   ```

5. **HTTP Request（メモ処理）**
   ```json
   設定：
   - Method: POST
   - URL: https://api.dify.ai/v1/workflows/run
   - Authentication: Header Auth
   - Body:
   {
     "inputs": {
       "original_text": "{{ $json.body.data.content }}"
     },
     "user": "n8n-workflow"
   }
   ```

6. **HTTP Request（Discord Bot返信）**
   ```json
   設定：
   - Method: POST
   - URL: https://your-railway-app.railway.app/draft-post
   - Body:
   {
     "channelId": "{{ $('Webhook').item.json.body.data.channelId }}",
     "draftContent": "{{ $json.data.outputs.text }}"
   }
   ```

---

## 🧠 STEP 5: Dify AI設定（30分）

### 5-1. Difyアカウント作成

![Dify初期画面](画像を挿入予定)

1. **[dify.ai](https://dify.ai)で無料アカウント作成**
2. **「Create App」→「Workflow」を選択**

### 5-2. URL記事要約ワークフロー作成

#### ワークフロー名：`URL記事→X投稿文`

**ノード構成：**

1. **Start（開始）**
   ```json
   Input変数:
   - news_url (String)
   - user_comment (String)
   ```

2. **HTTP Request（記事取得）**
   ```json
   設定：
   - Method: GET
   - URL: {{ news_url }}
   ```

3. **LLM（投稿文生成）**
   ```
   Model: GPT-4o-mini
   
   Prompt:
   以下の記事URLとユーザーコメントから、X(Twitter)用の投稿文を作成してください。

   記事URL: {{news_url}}
   ユーザーコメント: {{user_comment}}

   要件：
   - 280文字以内
   - 記事の要点を分かりやすく要約
   - 適切な絵文字を2-3個使用
   - 関連ハッシュタグを3-5個含める
   - 読みやすい改行と構成
   - ユーザーコメントの視点も反映

   投稿文のみを出力してください。
   ```

4. **End（終了）**
   ```json
   Output: text（生成された投稿文）
   ```

### 5-3. メモ→投稿文ワークフロー作成

#### ワークフロー名：`メモ→X投稿文`

1. **Start（開始）**
   ```json
   Input変数:
   - original_text (String)
   ```

2. **LLM（投稿文生成）**
   ```
   Prompt:
   以下のメモ内容からX(Twitter)用の投稿文を作成してください。

   メモ内容: {{original_text}}

   要件：
   - 280文字以内
   - メモの内容を読みやすく整理
   - 適切な絵文字を2-3個追加
   - 関連ハッシュタグを3-5個生成
   - 箇条書きや改行で視覚的に見やすく
   - 元の内容の意図を的確に表現

   投稿文のみを出力してください。
   ```

3. **End（終了）**

### 5-4. APIキー取得

1. **アカウントメニュー → 「API Keys」**
2. **「Create API Key」でキーを生成**
3. **キーをコピーして保存**

---

## 🔗 STEP 6: GitHub連携設定（10分）

### 6-1. リポジトリ作成

1. **[GitHub](https://github.com)で新しいリポジトリ作成**
   ```
   Repository name: Obsidian
   Public/Private: お好みで
   ```

2. **フォルダ構造を作成：**
   ```
   Obsidian/
   ├── 01.Clippings/
   │   ├── AI_News/
   │   └── Discord/
   ├── 03.Fleetings/
   │   ├── VoiceMemo/
   │   └── 議事録/
   └── README.md
   ```

### 6-2. Personal Access Token生成

1. **Settings → Developer settings → Personal access tokens**
2. **「Generate new token (classic)」**
3. **権限設定：**
   - ✅ repo（すべて）
4. **トークンをコピーして保存**

### 6-3. n8nでGitHub認証設定

1. **n8n Credentials → 「Add Credential」**
2. **「GitHub」を選択**
3. **Access Token貼り付け**

---

## 🧪 STEP 7: 最終接続とテスト（10分）

### 7-1. WebhookのURL取得と設定

![Webhook URL確認](画像を挿入予定)

1. **n8nで各ワークフローのWebhook URLをコピー**
   ```
   Obsidian保存用: https://your-instance.n8n.cloud/webhook-test/discord-reaction
   X投稿文生成用: https://your-instance.n8n.cloud/webhook/x-post
   ```

2. **RailwayのEnvironment Variablesに追加**
   ```
   N8N_WEBHOOK_URL = Obsidian保存用のURL
   N8N_X_POST_WEBHOOK_URL = X投稿文生成用のURL
   ```

3. **Railway Botを再起動**

### 7-2. 動作テスト

![テスト実行](動画を挿入予定)

1. **Discordでテストメッセージを投稿**
   ```
   これはテストメッセージです！
   AIについて学ぶのって楽しいですね。
   ```

2. **📝リアクションのテスト**
   - ✅が表示されたらObsidian保存成功
   - GitHubリポジトリを確認

3. **🐤リアクションのテスト**
   - AIが生成した投稿文がチャンネルに投稿される

4. **URL付きメッセージのテスト**
   ```
   https://example.com/ai-news
   この記事面白かったです！
   ```

---

## 🎯 トラブルシューティング

### よくあるエラーと解決法

| エラー | 原因 | 解決法 |
|--------|------|--------|
| Bot not responding | Discord Token間違い | Developer Portalで再生成 |
| 404 Error | Webhook URL間違い | n8nでURL再確認 |
| 401 Unauthorized | APIキー無効 | Dify/GitHubで新キー生成 |
| 403 Forbidden | GitHub権限不足 | Personal Access Tokenの権限確認 |
| Timeout | ワークフロー応答遅延 | Difyのモデル設定確認 |

### デバッグのポイント

1. **n8nワークフローの実行ログを確認**
2. **Railway/RenderのBot起動ログをチェック**
3. **Discord Developer Consoleでエラー確認**
4. **APIキーの有効期限と制限を確認**

---

## 🚀 カスタマイズアイデア

### 追加できる機能

#### 🎯 他のリアクション

```javascript
// index.jsに追加
else if (emoji === '📌') {
  // Notion保存
} else if (emoji === '📧') {
  // メール送信
} else if (emoji === '📅') {
  // カレンダー追加
}
```

#### 🔔 Slack連携

n8nに「Slack」ノードを追加して同時投稿

#### 📊 使用統計

Google Sheetsに使用回数や内容を自動記録

### プロンプトのカスタマイズ例

```
# カジュアルスタイル
友達に話すような親しみやすい口調で、絵文字を多めに使って...

# プロフェッショナルスタイル  
ビジネス向けの丁寧な文体で、専門的な内容を分かりやすく...

# 教育者スタイル
学びや気づきを共有する教育的な視点で、読者の成長を促すような...
```

---

## 🎉 まとめ：完成おめでとうございます！

![システム完成](画像を挿入予定)

お疲れさまでした！これで、**たった2つのリアクション**で以下が実現できるようになりました：

### ✅ 構築完了したシステム

- 📝 **Discord → Obsidian自動保存**
  - チャンネル別のフォルダ分類
  - 日時とメタデータの自動記録
  - GitHub連携による永続化

- 🐤 **Discord → AI投稿文生成**
  - URL記事の自動要約
  - メモから魅力的な投稿文作成
  - 最適なハッシュタグ自動生成

- 🔄 **完全自動化ワークフロー**
  - 0円で月数百回の処理が可能
  - 24時間365日稼働
  - スマホからでも操作可能

### 📈 今後の成長

このシステムをベースに、さらに発展させることができます：

1. **多様なSNSプラットフォーム対応**
2. **AI分析機能の追加**
3. **チーム共有機能の実装**
4. **定期レポートの自動生成**

### 🤝 サポートとコミュニティ

質問や改善案があれば、お気軽にご連絡ください：

- **Twitter**: [@tekitoo_T_cher](https://twitter.com/tekitoo_T_cher)
- **GitHub**: 実際のコードとファイルはこちら

### 📚 関連記事

- [前編：システム紹介](./Discordをハブにインプット・アウトプットを爆速化〜Dify×n8n×Discordボットシステム〜.md)
- [ObsidianとTodoist完全自動化](./ObsidianとTodoist同期を完全自動化した話%20-%20Automatorワークフローの奇跡.md)

---

**最後に**

この自動化システムにより、あなたの**思いつき→蓄積→発信**のサイクルが劇的に効率化されます。

毎日の小さな気づきが確実に価値あるアウトプットに変わる。
そんな「知識の循環システム」をぜひ活用してください！

**自動化は、創造性を解放する魔法です✨**

設定でつまずいた場合や、さらなるカスタマイズをしたい場合は、いつでもお声がけください。
一緒に、より良い学習・発信環境を作っていきましょう！