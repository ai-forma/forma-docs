# RuntimeClient

Used to determine what kind of client will be communicating with
this agent.

It can be used to switch from Streaming (SSE) or normal REST, and changing
the input/output schema.

> **Note** that this setting does not hot reload, meaning that; during development,
> you will need to stop and restart Forma for changes to be effective.


## Supported Variants

###  `sync`

Basic service-to-service communication, with no streaming.
Client sends an `LLMMessage`, and receives a new message back.



###  `sse`

Forma\'s Native SSE. The client sends an `LLMMessage`, and receives a
stream of `SSEvent`s back. If session persistence is enabled, the full conversation
will be stored/retrieved from the sessions database.



###  `ai-sdk-v5`

Streamed responses using Vercel\'s \'AI-SDK v5\' Server Side Events (SSE).
Client sends the native `AiSdkV5Input` request, and a stream of
SEEs is returned. No session\'s database is involved.



###  `ai-sdk-v5-persist`

Streamed responses using Vercel\'s \'AI-SDK v5\' Server Side Events (SSE).
Client sends a single message (the last user message) and the Forma agent
will take care of retrieving the full conversation from the sessions database,
if session persistence is enabled.



