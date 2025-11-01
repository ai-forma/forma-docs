# GenaiClient

Used to define which Generative AI Client will be
used to process information


## Supported Variants

> 🎯**Note**: Variants are identified by using the `provider` field. For instance 
>
> ```yaml
> provider: name-of-variant
> ```

* [`mock-l-l-m`](./auto-mockllm.md): A mock LLM
* [`openai-v1`](./auto-openaiv1.md): A client for OpenAI\'s v1 API
* [`ollama`](./auto-ollama.md): A client for Ollama
