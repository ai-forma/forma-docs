# Forma Agents' API Key

At present, Forma agents do not authenticate *users*. It is the calling service who should do that, get the ID, and then pass it along with the session id. However, Forma agents can require an API Key of your choice. You can opt out.

The steps to set an API key are the following:

## 1. Configure your Agent.

By default, agents will require an API Key. If you want to opt out, you need to enable the flag `client.no_api_key: true`

```yaml
id: dory 
client:
    no_api_key: true # <-- THIS
start:
  nodes:
    - llm:
        provider: ollama
      system_prompt: $/prompts/agent_prompt.md
```

## 2. Assign an API Key

If enabled, Forma will be expecting an environment variable called `FORMA_AGENT_KEY` to be available. This can be set in your `.env` file during development, and however you prefer in production. For example:

```sh
# Example of an API Key in an .env
FORMA_AGENT_KEY=key-not-for-production
```

## 3. Make requests

When making requests, make sure you add your API key using the API Key. For instance:

```sh
curl -X POST -i http://localhost:8080/v1/chat \
  -H "Authorization: Bearer key-not-for-production" \
  -H "X-User-ID: user-id" \
  -H "X-Session-ID: session-id" \
  -H "Content-Type: application/json" \
  -d '{"content":"hey"}'
```