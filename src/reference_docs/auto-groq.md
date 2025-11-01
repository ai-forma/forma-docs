# Groq

A client for Groq running in OpenaAI-compatible mode
(which happens by default)

It attempts to adhere as strictly as possible (even if
some features are not supported by Forma).

> 🔑 **Authentication**: uses the `GROQ_API_KEY` API Key

> Note: the documentation below has been copied nearly verbatim
> from OpenAI\'s one, as reference


## Full Specification

```yaml
endpoint: string
model: string
stream: boolean # optional
tools: 
	- OpenAITool
	- ... # optional
format: JsonSchema # optional
num_keep: int # optional
seed: int # optional
num_predict: int # optional
top_k: int # optional
top_p: number # optional
min_p: number # optional
typical_p: number # optional
repeat_last_n: int # optional
temperature: number # optional
repeat_penalty: number # optional
presence_penalty: number # optional
frequency_penalty: number # optional
stop: 
	- string
	- ... # optional
```

#### `endpoint`

The endpooint to utilize. Defaults to `http://127.0.0.1:11434`

#### `model`

The model to utilize. Defaults to `llama3.1:8b`

#### `stream` (*optional*)

If set to true, the model response data will be streamed
to the client as it is generated using server-sent events.
See the Streaming section below for more information,
along with the streaming responses guide for more information
on how to handle the streaming events.

#### `tools` (*optional*)

A list of tools the model may select as appropriate to call.

#### `format` (*optional*)

An object specifying the format that the model must output.

#### `num_keep` (*optional*)


#### `seed` (*optional*)


#### `num_predict` (*optional*)


#### `top_k` (*optional*)


#### `top_p` (*optional*)

An alternative to sampling with temperature, called nucleus sampling,
where the model considers the results of the tokens with top_p probability
mass. So 0.1 means only the tokens comprising the top 10% probability
mass are considered.

We generally recommend altering this or temperature but not both.s

#### `min_p` (*optional*)


#### `typical_p` (*optional*)


#### `repeat_last_n` (*optional*)


#### `temperature` (*optional*)


#### `repeat_penalty` (*optional*)


#### `presence_penalty` (*optional*)


#### `frequency_penalty` (*optional*)


#### `stop` (*optional*)



