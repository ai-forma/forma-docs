# Authenticating to LLM Providers

This is a work in progress as, more than authenticating to LLMs themselves, the approach is to authenticate to their provider. 

## API Keys

Some providers require API Keys. When this is the case, your API key should be available as an environment variable for Forma to look up. The name of the variable is specified [on their own docs](../reference_docs/auto-genaiclient.md).

## Other platforms

I am currently working on authenticating for Google... work in progress.