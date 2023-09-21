# [telegram](https://telegram.org/)
**需求是将消息发送到telegram对应的bot中，telegram中，每个都是bot，相当于channel**

[node-telegram-bot-api](https://github.com/yagop/node-telegram-bot-api)

使用 Telegram Bot 的完整流程包括创建 Bot、授权、获取 TARGET_CHAT_ID，并使用 Node.js 代码发送通知。以下是整个流程的步骤和示例代码：

1. 创建 Telegram Bot：
   - 打开 Telegram 应用，搜索 "BotFather"。
   - 与 BotFather 进行对话。
   - 使用 "/newbot" 命令创建一个新的 Bot。
   - 按照提示为 Bot 提供一个名称和用户名。
   - 成功创建后，BotFather 将提供一个 API Token，将其保存好，后续使用。

2. 授权 Bot：
   - 在 Telegram 应用中搜索你刚创建的 Bot 的用户名。
   - 与你的 Bot 进行对话（可以点击 "Start" 按钮）。
   - 这将授权你的账号与 Bot 进行通信，并使 Bot 能够发送消息给你。

3. 获取 TARGET_CHAT_ID：
   - 启动你的 Telegram Bot，并在对话中给 Bot 发送一条消息。
   - 在你的浏览器中访问以下链接，将 YOUR_BOT_TOKEN 替换为你的 Bot 的 API Token：
     ```
     https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
     ```
   - 在返回的 JSON 数据中，你可以找到 `chat` 对象中的 `id` 字段，该字段即为 TARGET_CHAT_ID。

4. 使用 Node.js 代码发送通知：
   - 在你的项目中安装 `node-telegram-bot-api` 库：
     ```bash
     npm install node-telegram-bot-api
     ```
   - 创建一个名为 `bot.js` 的文件，并添加以下代码：
     ```javascript
     const TelegramBot = require('node-telegram-bot-api');

     // 设置 Bot 的 API Token
     const botToken = 'YOUR_BOT_TOKEN';

     // 创建 Bot 实例
     const bot = new TelegramBot(botToken, { polling: true });

     // 发送通知
     const chatId = 'TARGET_CHAT_ID';  // 替换为你的 TARGET_CHAT_ID
     const message = 'Hello, Telegram!';  // 要发送的消息内容
     bot.sendMessage(chatId, message);
     ```
   - 将 `YOUR_BOT_TOKEN` 替换为你的 Bot 的 API Token，并将 `TARGET_CHAT_ID` 替换为你获取到的 TARGET_CHAT_ID。
   - 运行代码：
     ```bash
     node bot.js
     ```
   - 你的 Bot 将开始监听并向指定的聊天发送通知。
