# Workflows

As it was explained earlier, [workflows](../documentation/building-blocks.md#3-workflows) are a mechanism to break down large tasks into smaller ones. The value of this is that our system instructions will be shorter and more focused, meaning that LLMs will behave in a more predictable manner. Let's revisit the original example: 

> **Example**
> 
> We can break down this: 
> 
> ```
> Take this academic article and produce a blog post for 5th-graders, 
> in Spanish. 
>
> The content of the blog post should include a brief 
> introduction/motivation, a brief explanation of the methodology,
> and an emphasis in the results and implications.
>  
> Your target audience is 5th graders, so do not use acronyms or jargon.
> Use examples to make it more relatable.
> ```
> 
> Into these more focused steps
> 
> 1. `Create a list containing the (1) motivation; (2) methodology; (3) results and implications from the following paper` 
> 2. `Write a blog post for 5th graders based on the following summary points. Explain the motivation, outline the methodology and emphasise the results and implications. Use examples to make it more relatable.` 
> 3. `Translate this blog post into Spanish. Keep the tone and length of the post.`

I guess the motivation is clear enough. Let's get started.

## 1. Let's add more 