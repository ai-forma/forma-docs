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

Option to Not ask requests to contain an API Key. This API Key should be stored in `x-forma-key` header, and should match the environment variable `FORMA_AGENT_KEY`.


