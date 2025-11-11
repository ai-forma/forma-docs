# GenaiClient

Defines the LLM Provider, the model and the settings
utilise to generate responses


## Supported Variants

> 🎯 Variants are identified by using the `provider` field. For instance 
>
> ```yaml
> provider: name-of-variant
> ```

### [`ollama`](./auto-ollama.md)
A client for [Ollama](https://ollama.com) inference.

Ideal for running local processes in an easy manner during
development
### [`openai-v1`](./auto-openaiv1.md)
A client for [OpenAI\'s](https://openai.com) v1 API
### [`groq`](./auto-groq.md)
Client for [Groq](https://groq.com)
### [`vertex-ai`](./auto-vertexai.md)
Client for Google\'s [Vertex AI](https://cloud.google.com/vertex-ai) platform
