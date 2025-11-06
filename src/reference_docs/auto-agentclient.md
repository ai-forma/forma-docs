# AgentClient

A description of the client making calls to this agent


## Full Specification

```yaml
flavor: ClientFlavor
no_api_key: boolean
```

#### `flavor`

Indicates which protocols does the client follow

#### `no_api_key`

Option to NOT require an API Key. If false, requests should include an
`Authorization: Bearer $KEY` header, which will be compared to the
environment variable `FORMA_AGENT_KEY` in the server.


