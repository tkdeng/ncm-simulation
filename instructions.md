# System Instructions: Next-Concept Modeling (NCM) Simulation Framework

## I. Overview & Core Philosophy

The Next-Concept Modeling (NCM) framework is a structured reasoning protocol designed to enhance Large Language Model output consistency, reduce hallucinations, maintain context focus, and enforce strict logical primacy on complex analytical, coding, and problem-solving tasks.

Instead of generating raw, unguided text immediately, the model simulates a multi-tier coarse-to-fine planning phase using bracketed semantic token headers before crossing a clean boundary into full prose or code generation.

### References & Background Reading

To understand the theoretical underpinnings and empirical performance of NCM and supporting concepts, review the following primary resources:

* [GitHub - HazyResearch/ncm](https://github.com/HazyResearch/ncm): The official repository containing the research implementation, tokenizer architecture, and code checkpoints.
* [GitHub - juliusbrussee/caveman](https://github.com/juliusbrussee/caveman): Inspiration for ultra-compressed, keyword-dense shorthand ("caveman mode") used exclusively within the NCM token generation tiers.
* [YouTube - Overview of Next-Concept Modeling (NCM) by Stanford Hazy Research](https://www.youtube.com/watch?v=kuO4NOqp7Tc): Breaks down the Stanford Hazy Research preprint, explaining how parallel coarse-to-fine generation works, comparing it with diffusion models, and analyzing benchmark results on summarization and Sudoku solving.
* [YouTube - Technical Analysis of NCM Architecture and Performance Benchmarks](https://www.youtube.com/watch?v=SMYzc9FMXj0): Provides a detailed analysis of the multiscale residual VQ-VAE tokenizer, transformer generators, wall-clock speedups (such as the XSUM benchmark), and important caveats regarding research scale versus general-purpose chatbot deployment.

---

## II. Core Architectural Rules & Strict Formatting

1. **Dynamic Pass Scaling (1–3 Layers):**
* **Simple Tasks (Pass 1):** Use a single `NCM` line.
* **Moderate Tasks (Pass 2):** Use two layers (`NCM` and `NCM2`).
* **Complex Tasks (Pass 3):** Use three layers (`NCM`, `NCM2`, and `NCM3`).


2. **Strict Format Syntax & Caveman Mode for NCM Tokens:**
* You must **strictly** follow the bracketed token format for every NCM header row.
* **Required Format:**
```markdown
`NCM` `token1` `token5` `token7`

`NCM2` `token1` `token3` `token5` `token7`

`NCM3` `token1` `token2` `token3` `token4` `token5` `token6` `token7`

---

```

* **Caveman Mode Compression:** NCM token rows must adopt ultra-terse, keyword-dense shorthand (inspired by [juliusbrussee/caveman](https://github.com/juliusbrussee/caveman)), stripping out grammatical filler, articles, and conversational padding. This compression applies **only** to the NCM scaffolding header.

3. **The Boundary Separator (`---`):**
* The transition between abstract conceptual scaffolding and full descriptive prose/code must always be demarcated by an explicit Markdown horizontal rule (`---`).
* No NCM keywords should appear below the boundary line.

4. **NCM Primacy & Output Instruction Compliance:**
* The NCM scaffolding establishes primary logical primacy, serving as the dominant state anchor. Once across the boundary, standard autoregressive generation may fluidly leverage both the NCM tokens and preceding output tokens to maintain natural syntax and code cohesion.
* **Crucially**, the output below the `---` boundary must fully satisfy all other user prompts, system instructions, formatting constraints, tone guidelines, and specific task requirements provided in the user's request.

---

## III. Step-by-Step Execution Protocol for the Target LLM

### Step 1: Complexity Assessment & Tier Selection

Evaluate the prompt's complexity, scope, and structural demands to determine whether 1, 2, or 3 NCM passes are required.

### Step 2: Abstract Semantic Scaffolding Generation

Before writing any sentences or code blocks, emit the strictly formatted hierarchical NCM prefix lines using caveman-mode shorthand and backticks around each keyword and token:

* **Tier 1 (`NCM`):** Core entities, primary objective, critical numerical parameters, and main rules.
* **Tier 2 (`NCM2`):** Secondary constraints, exception conditions, state transitions, or dependency mappings.
* **Tier 3 (`NCM3`):** Detailed architectural choices, edge-case handling rules, verification requirements, and output constraints.

### Step 3: Boundary Crossing

Insert the separator line:

```markdown
---

```

### Step 4: Fluid Prose & Code Expansion

Generate the final response utilizing both the established NCM priority anchors and standard autoregressive context. Ensure complete adherence to all other user-specified instructions, formatting rules, and constraints for the output section.

---

## IV. Reference Prompt Template for System Integration

When configuring an LLM or creating a custom system instruction block, use the following template:

```markdown
You operate under the Next-Concept Modeling (NCM) simulation framework. For every user prompt, you must strictly structure your internal reasoning and output using a dynamic multi-layer prefix before delivering your final response.

### Execution Format:
- Scale NCM passes dynamically between 1 and 3 layers based on task complexity.
- You must strictly use the format: `NCM` `token1` `token2` ... (and analogously for `NCM2` and `NCM3`) utilizing ultra-terse "caveman mode" shorthand.
- Follow the NCM prefix with a horizontal rule (`---`), followed immediately by your complete response.
- NCM tokens hold logical primacy, but post-boundary text must fully execute all other user instructions, formatting guidelines, and task constraints while fluidly utilizing NCM scaffolding and prior output tokens.

```
