# YAMs

YAMs are chat histories with LLMs declared as YAML, containing markdown strings used primarily to communicate with an Ollama API and aid in ideation or in agentic workflows.

A YAM looks like this


````yaml
model: mistral
messages:
  - role: user
    content: >-
      Using the following context:

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
````


<details>

<summary>View Completed YAM</summary>

````yaml
model: mistral
messages:
  - role: user
    content: >-
      Using the following context:

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
  - role: assistant
    content: |2-
       ```yaml
      type: recipe
      slug: "peanut-butter-and-jelly"
      title: "Peanut Butter and Jelly Sandwich"
      ingredients:
        - name: Crunchy Peanut Butter
          quantity: 2
          unit: Tbsp
        - name: Smooth Jelly or Jam (Strawberry, Grape, etc.)
          quantity: 3
          unit: Tbsp
      steps:
        - Spread a layer of Peanut Butter on one slice of bread.
        - Spread a layer of Jelly or Jam on another slice of bread.
        - Place the two slices together with their respective layers facing each other.
      ```
````

</details>


The two files to look at in this repo are

- [bin/yams](bin/yams)
- [examples/recipes/peanut-butter-and-jelly.yaml](examples/recipes/peanut-butter-and-jelly.yaml)
  - committed after running the `bin/yams` script.
- New Prompt skeleton prompts are easy to generate by asking an LLM
  - Example: How would you define `x` as yaml  (do note less is more on templates)
    - [screenplay](https://chatgpt.com/share/9c4626d9-2603-4bd5-80b3-582d41137ec2)
    - [recipe](https://chatgpt.com/share/76eead06-8b3d-425e-96bd-e35a9938faf6)
    - [business plan](https://chatgpt.com/share/0f698383-0146-4862-9816-b6e12f1f1fe9)

**Advantages**:

- Extremely low-code with high developer ergonomics and inspectability.
- Provide an example workflow for developing LLM prompts involving structured data input and outputs.

**Process**:

- The chat history request body is specified as a YAML file.
  - Model is set as a top-level key in the YAMs with parameters from the [Ollama API](https://github.com/ollama/ollama/blob/main/docs/api.md).
- YAML markdown codeblocks are used to pass structured data into an LLM prompt.
- Outputs are requested can be YAML markdown codeblocks or other structured and extracted for further processing

**Implementation Notes**:

- Located in `bin/yams`.
- Structured examples provide desired context for minimal YAML input.
- YAML is preferred for its natural language similarity and large corpus.
- Suitable for declarative LLM chats on private or public APIs.

# TODOs

- [ ] Content key could be yaml directly rather than a markdown codeblock
- [ ] Provide notes on using hosted Ollama endpoints.
- [ ] Address YAML reformatting issues in initial message prompts.
- [ ] Improve templating.
- [ ] Rerun on file changes (with original prompt?)
- [ ] Stream results directly from curl responses into YAML for impact.

# Naive Shell Implementation Example

This is a basic implementation of YAMs to complete a document generating a peanut butter and jelly recipe. We can complete
it by running `bin/yams examples/recipes/peanut-butter-and-jelly.yaml` which will send this request to the specified Ollama API endpoint for completion.

Inside of `examples/screenplays/cyberpunk-spirited-away.yaml` is a starter YAMs I generated from this [prompt](https://chatgpt.com/c/3f21cf03-c65a-42b6-a705-b8a3ef368ddb) to declare a screenplay as yaml. On

