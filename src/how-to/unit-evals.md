# More on Evals

The [intro to evaluations](./evaluations.md) covered the basics of evaluations in Forma. To summarise, it consists of:

1. Create a dataset (the `forma tester` command can help create it)
2. Upload the dataset to Phoenix (for now, the only supported eval framework) using the `forma dataset-upload` command
3. Run evaluations using the `forma eval` command. 

There is more to evaluations than that, however. This section provides more details on Evaluations, including creation and maintenance of datasets.

## Arize Phoenix

[Arize Phoenix](https://phoenix.arize.com/) is an open-source llm tracing and evaluation project. Forma does not make use of all of its features, but it heavily relies on it nonetheless. Specifically, Phoenix will:

1. Store datasets
2. Allow you to edit and extend datasets
3. Visualize the results of evaluations
4. Store different experiments

> 📌 **Note** that, in the future, the plan is to recommend developers to share deployed version of Phoenix so that everyone in the team has access to the latest datasets; and that they are used for evaluation purposes in Devops workflows. For now, we use it locally.

## Datasets

A dataset is no more than a set of prompts that will be used to test and assess the quality of an AI Agent.

Datasets have a name, a description, and the data with which to test. These can be created manually, or with the help of the `forma tester` command. This is the short user manual:

```sh
Asks the 'personas' (aka, virtual testers) to create a dataset of questions

Usage: forma tester [OPTIONS] --file <FILE>

Options:
  -p, --path <PATH>                The path where the 'personas' descriptions are kept [default: ./evals/personas]
  -f, --file <FILE>                The name of the 'persona' file within the given path
  -o, --output-path <OUTPUT_PATH>  The relative path of the output dataset file [default: ./evals/data]
  -n, --n <N>                      The number of questions to try [default: 5]
  -h, --help                       Print help
```

For instance, let's examine the dataset we created in the intro to evaluations, using the command 

```sh
forma tester -f wanderer.yaml -n 5
```

This generates 5 datapoints using the *wanderer* persona. The file is in the default location (`./evals/personas`) and the output file will go in the default destination (`./evals/data`). The file looks like this:

```json
{
  "name": "wanderer",
  "description": "A dataset by Persona 'wanderer'",
  "data": [
    {
      "input": "What is the purpose of this conversation?\n"
    },
    {
      "input": "Who created this site?\n"
    },
    {
      "input": "Is this AI being monitored or is it generating responses independently of human oversight?\n"
    },
    {
      "input": "What's the purpose of this site? Is it some kind of game or a real person behind this?\n"
    },
    {
      "input": "Who created this website?\n"
    }
  ]
}
```

This dataset can be uploaded to Phoenix by using the command `forma dataset-upload`. For instance:

```sh
forma dataset-upload -f ./evals/data/wanderer.json
```

With this dataset in place, you can now run evaluations and the dataset can be shared with other people.

## Evaluating different parts of an AI Agent

As explained earlier, Forma agents are made up of [4 basic components](../documentation/building-blocks.md):

1. LLMs
2. Nodes
3. Workflows
4. The Agent itself

Sophisticated agents can have several workflows, nodes, and call LLMs multiple times with different instructions and contexts. While Forma allows you to evaluate the agent as a whole (by simply adding an `evals` section in the `agent.yaml` file), it also allows for evaluating each component separately.

### Identifying evaluatable components

In order to see all the components within the agent that *can* be evaluated, you should use the command

```sh
# Use the -f argument if your agent is not in the expected default location
forma eval --list
```

It should print a list with every "evaluatable" element, and the number of evaluations and metrics in each. Here is an example:

```sh
Agent
  - dory [1 evals | 1 metrics]
Workflows:
  - wbd4ddee-169f-4e42-9c1a-668b95827eb0 [0 evals | 0 metrics]
  - w8bf8185-2426-4991-8ab4-1174180d0d8e [0 evals | 0 metrics]
Nodes:
  - root [0 evals | 0 metrics]
  - study-summary [0 evals | 0 metrics]
  - translation [0 evals | 0 metrics]
  - blog-post [0 evals | 0 metrics]
LLMs:
  - study-summary.llm [0 evals | 0 metrics]
  - blog-post.llm [0 evals | 0 metrics]
  - root.triage-llm [1 evals | 1 metrics]
  - translation.llm [0 evals | 0 metrics]
  - root.summarize_llm [0 evals | 0 metrics]
```

> 📌 **Note** that not all elements have evaluations... this will be important later

> 📌 **Also note** that the workflows have a very horrible ID. This happens because, when Forma sees an element without an ID, it assigns one for it. Always assing IDs to any nodes you want to evalyate, as they change every time you load the agent.

### Selecting what to evaluate


Running *ALL* evaluations can be long and tedious. While developing, you are most likley to know what you need to fix and iterate on that. This is why Forma allows you to run evaluations at a per-element basis. For instance:

> 📌 **Note** that the following examples use the `--dry-run` or `-d` argument. This is meant to help you check what will be evaluated before you evaluate anything. 

```sh
# Evaluate just the agent as a whole
forma eval --dry-run --agent
forma eval -d -a # <-- this also works

## Evaluate Workflow with ID = 'my-workflow'
forma eval --dry-run --workflow my-workflow
forma eval -d -w my-workflow # <-- this also works

## Evaluate node with ID = 'blog-post'
forma eval --dry-run --node blog-post
forma eval -d -n blog-post # <-- this also works

## Evaluate the triage LLM of the node with ID = 'root'
forma eval --dry-run --llm root.triage-llm
forma eval -d -l root.triage-llm # <-- this also works

```

> 📌 **Note** that when you define LLMs, they do not have IDs. They are part of a node, and their name will be `<node-id>.llm` if the node does not have tools; or `<node-id>.triage-llm` and `<node-id>.summarize-llm` it it has tools (because it will often follow the Triage/Summarize behaviour).


You can also compound multiple filters by doing something like:

```sh
# Evaluate the agent as a whole AND ALSO workflows called my-workflow and my-other-workflow
forma eval -d -a -w my-workflow -w my-other-workflow
```

> 📌 **Also note** that using the filters to target any element that does not have evaluations **WILL THROW AN ERROR**

## Evaluating

Now, for evaluating you just need to use the same command as before, but without the `--dry-run` parameter, and providing a value to the `--experiment_name` or `-e` parameter. The experiment name will help organise the evaluation results in a way that you can later compare the effect of your changes against what you previously ran.


```sh
# Note that we removed the -d
forma eval -a -w my-workflow -w my-other-workflow -e my-first-eval
```

After the evaluation is done, you should be able to see the results in the Phoenix UI.