# Exercise 1 - Open source for the win!

## Goal

You will use the public EGA v2 sources and an online language model as learning aids.

## Prerequisites

You need GitHub access and some kind of Large Language Model (LLM) with internet access.

## Instructions

1. Open the validation tool ([Biovalidator](https://github.com/EbiEga/biovalidator)) and the validation schemas ([JSON Schemas](https://github.com/EGA-archive/fega-metadata-schema)).

   Note how all information pertaining to these two are open-source and public: if you can see it, so can LLMs (_for the most part_).

2. Open your preferred LLM, enable its internet access skill/feature, and copy this prompt (or similar) into your online language model:

   ```text
   @Web search I'm not familiar with metadata validation. What are the EGA v2 JSON Schemas (https://github.com/EGA-archive/fega-metadata-schema) for? What is being validated? By what standards? Be brief and provide mock examples.
   ```

   The [shared ChatGPT conversation](https://chatgpt.com/share/6a6b39b7-3818-83eb-a6c9-3ec47b29a3ec) is an example of how it would look like.

3. Open every source link in the answer and check supports the claim. An LLM can help you understand a concept, but you definitely should not blindly trust it. 

## Questions

1. Which source do you trust if the model and the repository disagree?
2. How can an LLM help you onboard this project?
3. What are, broadly, the benefits of open-source repositories?

> **In the real repository:** start from the [technical report](https://github.com/EGA-archive/fega-metadata-schema/blob/main/docs/FEGA-metadata-technical-report.md), root [README](https://github.com/EGA-archive/fega-metadata-schema/blob/main/README.md), and [release guide](https://github.com/EGA-archive/fega-metadata-schema/blob/main/docs/releases/README.md).

<details>
<summary>Solution</summary>

1. The versioned repository source wins. A language model can help you find and explain information, but it does not replace the source.
2. An LLM can summarize documentation, explain unfamiliar concepts, locate relevant files and links, and suggest a path through the project. Its answers and sources should be checked against the repository, though.
3. Open-source repositories provide **transparency**, peer review, reusable code and documentation, **collaborative improvement**, and the ability to **inspect, adapt, and verify** the implementation.

</details>

## Concept summary

With open source, you can read both the code and the reasons behind it. A language model can make that material easier for you to navigate.

You should still check each important claim against the exact source and version.
