# FormaRuntime

Configures


## Full Specification

```yaml
client: RuntimeClient
persist_sessions: boolean
no_api_key: boolean
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


