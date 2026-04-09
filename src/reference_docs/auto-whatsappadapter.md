# WhatsappAdapter

Adapter for the WhatsApp API. THIS IS VERY EXPERIMENTAL


## Full Specification

```yaml
host_phone_number: string
whatsapp_api_key: string
max_history_messages: int
```

#### `host_phone_number`

The phone number associated with the account

#### `whatsapp_api_key`

The API key to authenticate

#### `max_history_messages`

The maximum number of messages to retrieve from the
sessions database in each user interaction. The purpose
is to prevent (1) the system prompt from being diluted by
a large number of messages, and (2) reduce the token usage.


