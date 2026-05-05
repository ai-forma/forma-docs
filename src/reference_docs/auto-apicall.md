# ApiCall

A tool that makes HTTP REST API calls.

Forma sends the request on behalf of the LLM once it has decided the
argument values. The LLM fills in:

- URL path parameters — declared inline in `url` using the same
  `{{name: type \"description\"}}` template syntax used elsewhere in Forma
- Request body fields — declared via the `body` JSON schema

Secrets can be passed as header values using `$VAR_NAME` or `${VAR_NAME}`:
they are resolved from environment variables at runtime so they never need
to appear in config files.

Example (YAML):
```yaml
type: api-call
url: \'https://api.example.com/users/{{user_id: string \"the user to look up\"}}\'
method: GET
headers:
  Authorization: \"$API_TOKEN\"
```


## Full Specification

```yaml
url: string
method: string
headers: HashMap
body: JsonSchema # optional
```

#### `url`

The endpoint URL. Path parameters the LLM should fill are declared
using `{{name: type \"description\"}}` — the same template syntax used
elsewhere in Forma. For example:
`https://api.example.com/users/{{user_id: string \"the user\'s ID\"}}`

Supported types for URL parameters: `string`, `integer`, `number`, `boolean`.

#### `method`

HTTP method. Case-insensitive (e.g. `GET`, `post`, `Put`).
Supported values: GET, POST, PUT, DELETE, PATCH, HEAD.

> Defaults to `GET`.

#### `headers`

HTTP headers to attach to every request.
Values starting with `$` are resolved from environment variables:
`\"$TOKEN\"` or `\"${TOKEN}\"` → value of the `TOKEN` env var.

#### `body` (*optional*)

Schema for the JSON request body. Must be an `object` schema.
Omit for requests that carry no body (e.g. GET).
The LLM will provide values for all fields described here.


