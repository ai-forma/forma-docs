# AI Agents' Memory

AI Agents are generally thought to have two kinds of memory:

1. **Short-term (or "contextual") memory**
2. **Long-term memory**
3. **Working memory**


These two play very different roles. Short-term memory lets an agent carry a coherent conversation or reasoning process. Long-term memory, on the other hand, lets it *remember* information beyond a single session — preferences, facts, or outcomes that matter later.



## Short-term or "contextual" memory

> *"Chatbots without contextual memory just suck... there, that’s the quote."*

Short-term or **contextual memory** is critical for ensuring a natural and continuous interaction. Without it, every exchange—your question and the agent’s response—stands completely alone, like talking to someone with a 3-second attention span.

Here’s a simple example:

```
Hello. I would like an espresso, to take away, please.

        Sure thing. What is your name?

Peter.

        Hi, Peter. What are you after?

??? ... I am Peter, and I want an espresso, to take away, please.

        Sure thing, Peter. Here it is.

Thanks. Can I also get a cookie?

        Sure thing! What is your name?
```

If that chat sounds frustrating, it’s because it *is*. Humans automatically interpret language in context. Every sentence we say or hear connects to what came before — words, tone, even shared experience. Without context, language loses meaning.

For **LLMs**, though, context isn’t natural or implicit. It must be *provided*. When you talk to a language model, each response is generated based only on the text it sees in that moment. If you want the agent to “remember” previous messages, you have to include them explicitly in the prompt. That’s what short-term memory is: **a structured way to feed the model its own conversational history**.

Practically speaking, contextual memory often looks like this:

* The messages of a conversation are stored within a database
* Every time a user sends a message, the conversation is retrieved from this database, and expanded with the user message and send to the LLM (so it can undertand the new message within a context)
* The model then generates an answer *as if* it remembered the whole conversation... but truly, we need to provide it every time

In summary, “giving the agent a short-term memory” really means “let's maintain the history of the conversation somewhere and feed it back each time.” And thus, while the *intelligence* comes from the LLM's training, the *continuity* comes from your memory implementation.


> **Note** This design works well up to a point — usually limited by the model’s **context window** (the maximum number of tokens it can process at once). Beyond that, messages must be summarized, compressed, or dropped. In my experience, you can keep the last N (e.g., 25?) messages and conversation might still feel natural.


## Long-term memory

While contextual memory is about the a single conversation itself (e.g., like talking to a stranger at the bus stop), long term memory is about knowledge that is kept *between* conversations.

For example, if you ask "I need a new job, what would you suggest?, an AI Agent *without* long-term memory will say "Tell me about yourself" (or something). On the contrary, one *with* long-term memory might say "based on our chats, I think...". 

The first one is starting from scratch. It does not know you. The second one remembers you.

Some people argue that long-term memory is what makes an AI assistant truly useful. That’s debatable. Not every agent needs to remember things about you. I don’t want the person at the immigration booth to remember me next time. I just need them to do their job, and I am tired. And that’s perfectly fine.

But for AI Agents that *live with you* (e.g., on your phone, your desktop, or inside your daily workflow) long-term memory unlocks a different level of usefulness. It lets them recognize patterns, recall past interactions, and feel more personal.

As a rule of thumb:

* If you’re building a **transactional AI assistant** (something that helps people get specific tasks done, like booking a dentist appointment or submitting a form), long-term memory isn’t essential.
* If you’re building a **personal AI companion or assistant**—something meant to grow with the user—then long-term memory becomes crucial.

## Working memory

