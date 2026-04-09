# TelegramAdapter

Adapter for the Telegram Bot API.

Registers a single webhook endpoint that receives [`TelegramUpdate`]s and
replies through the [Telegram Bot API](https://core.telegram.org/bots/api).

Set the webhook URL on your bot with:
```text
https://api.telegram.org/bot{TOKEN}/setWebhook?url=https://your-host/v1/chat
```

### Required environment variables
* `TELEGRAM_BOT_TOKEN` — the token provided by @BotFather.


## Full Specification

```yaml
max_history_messages: int
bot_token: string
accept_button_text: string
reject_button_text: string
confirm_tool_call_question: string
```

#### `max_history_messages`

Maximum number of past messages included in each context window.

#### `bot_token`

Populated from the `TELEGRAM_BOT_TOKEN` env var during [`init`](Self::init).

#### `accept_button_text`

Text to come up in the `accept tool call` button. Defaults to `\"Yes\"`.

#### `reject_button_text`

Text to come up in the `reject tool call` button. Defaults to `\"No\"`.

#### `confirm_tool_call_question`

Text to come up in the `confirm tool call` button. Defaults to `\"Approve this action?\"`.


