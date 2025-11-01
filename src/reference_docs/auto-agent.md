# Agent

Defines the entry points, evaluations and other settings
for the Forma agent.


## Full Specification

```yaml
id: string
start: Workflow
evals: 
	- Eval
	- ...
persist_sessions: boolean
client: AgentClient
```

#### `id`

The ID. If absent, one will be provided.

#### `start`

The Workflow that serves as a starting point of this Agent.

#### `evals`

The evaluations that will be used to test the
Agent as a whole.

#### `persist_sessions`

If true, the Agent will keep the state and the history of the
conversation in a MongoDB-compatible database.

#### `client`

Options for adapting Forma agents to different
clients.


