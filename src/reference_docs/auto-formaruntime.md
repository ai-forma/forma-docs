# FormaRuntime

Configures the application wrapping the AI Agent.


## Full Specification

```yaml
client: RuntimeClient
persist_sessions: boolean
no_api_key: boolean
max_history_messages: int
```

#### `client`

Options for adapting Forma agents to different
clients.

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


