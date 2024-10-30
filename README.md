# Automatic Petri Net Generation from Text

This repository provides code for automatically generating Petri nets from textual process descriptions. The method leverages Large Language Models (LLMs) to understand the semantics of the text and translate it into the formal structure of a Petri net.

## Method and Features

This method addresses the challenges of LLM-based process modeling, specifically in handling complex structures and ambiguities in process descriptions.  It utilizes a two-step approach:

1. **Pre-processing:** This step structures the input text to minimize ambiguities and inconsistencies.  It involves:
    * **Clarification Questions:** The LLM generates questions to the user to clarify missing or ambiguous information in the process description.  This human-in-the-loop approach ensures a more complete and accurate understanding of the process.
    * **Structuring:** The enhanced process description is then structured into predefined sections (e.g., process start, sequential section, parallel section, decision, loop, process end) to facilitate the subsequent model generation step. This structuring mimics rule-based approaches, making the process more predictable and reliable.

2. **Model Generation:** The structured process description is processed by the LLM to generate a JSON representation of the Petri net.  Two versions are implemented:
    * **Version 1 (Holistic):** The entire structured description is processed at once.  This allows the LLM to consider the full context but requires it to handle multiple workflow patterns simultaneously.
    * **Version 2 (Stepwise):** The structured description is divided into sections, and each section is modeled independently.  This simplifies the modeling of individual sections but adds complexity in connecting the resulting sub-models.

    Both versions utilize a **self-feedback mechanism** where the LLM critiques and refines its generated output, minimizing errors and improving the quality of the final Petri net.  The final output is a JSON file conforming to the chosen modeling tool's specifications.

## Key Prompt Engineering Techniques

Several prompt engineering techniques are employed to guide the LLM:

* **Role Prompting:** The LLM is assigned the role of a "process modeling expert."
* **Knowledge Injection:**  Domain-specific knowledge about Petri nets and workflow patterns is provided.
* **Few-Shot Prompting:** Examples of correct process models are provided.
* **Negative Prompting (for clarification questions only):** Examples of what *not* to do are provided.
* **XML Formatting (for structuring and modeling):**  XML is used to structure complex prompts.
