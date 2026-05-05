# FormaRuntime

Used to determine what kind of client will be communicating with
this agent.

It can be used to switch from Streaming (SSE) or normal REST, and changing
the input/output schema.

> **Note** that this setting does not hot reload, meaning that; during development,
> you will need to stop and restart Forma for changes to be effective.


## Supported Variants

> 🎯 Variants are identified by using the `client` field. For instance 
>
> ```yaml
> client: name-of-variant
> ```

### [`sync`](./auto-openaisyncadapter.md)
Basic service-to-service communication, with no streaming.
Client sends an `Open AI Message`, and receives another back.

This is meant to work mostly for machine-to-machine communication, where
the client is a server, that needs to submit tasks or questions to
a Forma Agent.
### [`sse`](./auto-openaisseadapter.md)
Basic service-to-service communication, with streaming of states (not tokens).
Client sends an `Open AI Message`, and receives updates with respect
to tool calls and other state changes.

This is meant to work mostly for machine-to-machine communication, where
the client is a server, that needs to submit tasks or questions to
a Forma Agent.
### [`ai-sdk-v5`](./auto-aisdkv5adapter.md)
Streamed responses using Vercel\'s \'AI-SDK v5\' Server Side Events (SSE).
Client sends a single message (the last user message) and the Forma agent
will take care of retrieving the full conversation from the sessions database,
if session persistence is enabled.

Note that sending only the last message is NOT AiSDK\'s normal behaviour.
The default behaviour of the Vercel AI SDK v5 is to send the whole conversation
on every interaction. Forma does not favour this behaviour.

> Note: In trying to add compatibility with v6\'s Human in the loop,
> we noticed that Vercel\'s docs seem inconsistent or out of date.
> Therefore, human-in-the-loop compatibility is implemented without
> streaming.
### [`whatsapp`](./auto-whatsappadapter.md)
Use your Forma Agent as a Webhook for a [Whatsapp Cloud API](https://developers.facebook.com/documentation/business-messaging/whatsapp/about-the-platform).

THIS HAS NOT BEEN TESTED YET PROPERLY.

This runtime always persist sessions.

> *Note* that connecting to real webhooks while developing
> your agent will require [Ngrok](https://ngrok.com/) or a similar product.
> However—because the runtime does not change the behaviour of your agent—you
> can test your agent using any other kind of client service

### Authentication

Set the following environment variables.

```bash
WHATSAPP_HOST_NUMBER_ID=123123123
WHATSAPP_KEY=whatsapp-long-token # For authenticating with the Whatsapp API
WHATSAPP_VERIFY_TOKEN=12321 # for verifying webhooks
```
#### How Whatsapp messages are translated into LLM Messages
### [`telegram`](./auto-telegramadapter.md)
Use your Forma Agent as a Telegram Bot webhook.

This runtime always persists sessions. Each Telegram chat maps to one
session; the chat ID is used as the user identifier.

Register the webhook with Telegram once your server is reachable:
```text
https://api.telegram.org/bot{TOKEN}/setWebhook?url=https://your-host/v1/chat
```

### Human in the loop

Human in the loop is surfaced as a message with two inline
buttons: Accept or Reject. These can be set up through the
`accept_button_text` and `reject_button_text` configuration
options.

### Authentication

Set the following environment variables.

```bash
TELEGRAM_BOT_TOKEN=your-telegram-bot-token # the token obtained from @BotFather.
```
