# AiSdkV5Adapter

Meant to be called from the Vercel AI SDK v5-compatible client.

It offers 3 basic endpoints:
- `v1/init` to initiate a session
- `v1/chat` to send a message and get a streamed response
- `v1/resume` to resume a session

Note that `v1/resume` does not use SSE streaming, but a synchronous response.
This is due to some issues we found when trying to incorporate v6 and human-in-the-loop
capabilities. [Issue here (not by us)](https://github.com/vercel/ai/issues/9980)


## Full Specification

```yaml
persist_sessions: boolean
no_api_key: boolean
max_history_messages: int
```

#### `persist_sessions`

If true, the Agent will keep the state and the history of the
conversation in a MongoDB-compatible database.

#### `no_api_key`

Option to NOT require an API Key. If false, requests should include an
`Authorization: Bearer $KEY` header, which will be compared to the
environment variable `FORMA_AGENT_KEY` in the server.

#### `max_history_messages`

The maximum number of messages to retrieve from the
sessions database in each user interaction. The purpose
is to prevent (1) the system prompt from being diluted by
a large number of messages, and (2) reduce the token usage.


