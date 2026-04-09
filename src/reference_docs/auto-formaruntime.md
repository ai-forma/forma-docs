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
Client sends an `FormaMessage`, and receives a new message back.
### [`sse`](./auto-openaisseadapter.md)
Forma\'s Native SSE. The client sends an `FormaMessage`, and receives a
stream of `SSEvent`s back. If session persistence is enabled, the full conversation
will be stored/retrieved from the sessions database.
### [`ai-sdk-v5`](./auto-aisdkv5adapter.md)
Streamed responses using Vercel\'s \'AI-SDK v5\' Server Side Events (SSE).
Client sends a single message (the last user message) and the Forma agent
will take care of retrieving the full conversation from the sessions database,
if session persistence is enabled.

> Note: This is NOT the normal behaviour. The default behaviour
> of the Vercel AI SDK v 5 is to send the whole conversation
> on every interaction. Forma does not favour this behaviour.
### [`whatsapp`](./auto-whatsappadapter.md)
Use your Forma Agent as a Webhook for a [Whatsapp Cloud API](https://developers.facebook.com/documentation/business-messaging/whatsapp/about-the-platform).

THIS HAS NOT BEEN TESTED YET.

This runtime always persist sessions.

> *Note* that connecting to real webhooks while developing
> your agent will require [Ngrok](https://ngrok.com/) or a similar product.
> However—because the runtime does not change the behaviour of your agent—you
> can test your agent using any other kind of client service

### Authentication

#### How Whatsapp messages are translated into LLM Messages
