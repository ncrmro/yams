# YAMs
YAMs are LLM chat histories declared as yaml (with markdown strings).

The benefit of this approach is it's extremely low code with high level of (developer) user ergonomics and inspectability

YAMs as a process.

* The chat history (Ollama) request Body is specified as a YAML file
* ([Ollama](https://github.com/ollama/ollama/blob/main/docs/api.md)) API Parameters 
* YAML Markdown Codeblock (strings) are used to pass structured data as context into an LLM prompt (specified as multiline yaml string which is actually markdown).
* We can use this for the bases of our output we again ask for as a yaml markdown codeblock
* Using regex we can extract this returned codeblock then parse with YQ
  * any errors are added to the chart history and then sent to the LLM asking a follow up.

---

Everything the follows is in the context of using the naive shell implementation of YAMs located at `bin/yams`.

* We could provide a more fleshed out example to give the LLM the structure we desire before passing in a more minimal yaml context block
* we also specify our output yaml is desirable here again because it's large corpus and similarity to natural language (compared to say json or actual coding languages)
* They allow for a declarative LLM chats ran on private or public APIs

# TODOs

- [] Something is reformating the yaml in the initial messages's promp's markdown context.
- [] Better Templating
- [] Stream results directly from curl response into the yaml (for that wow factor)

# Naive Shell Implementation Example

Note the example at the time of writing is a naive implementation of YAMs and shell and leaves a lot to be desired!

- [examples/recipes/peanut-butter-and-jelly.yaml](examples/recipes/peanut-butter-and-jelly.yaml) (this one is commited after rerunning the script with only the first message)
- examples/recipes


```yaml
model: mistral
messages:
  - role: user
    content: >-
      Using the following context.

      ```yaml 
      type: recipe
      slug: ""
      title: "Peanut butter and jelly"
      ingredients:
        - name: Crunchy Peanut Butter
          quantity: 2
          unit: Tbsp
      steps:
        - Spread Peanut Butter on bread.
      ```

      Complete the document in the YAML code block.

      ```yaml

      ```
```