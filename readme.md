# NCM Simulation

A system prompt designed to allow an LLM to simulate a **Next-Concept Modeling (NCM)** coarse-to-fine planning architecture.

### What is NCM?
NCM is a coarse-to-fine planning framework that replaces standard left-to-right token generation with a hierarchical reasoning process. Inspired by research from [Stanford Hazy Research](https://github.com/HazyResearch/ncm), it forces the LLM to map out high-level concepts, constraints, and dependencies as compressed semantic tokens before generating the main response. 

By requiring the model to commit to explicit planning tokens before writing prose or code, the prompt establishes a strict logical boundary. This upfront structural commitment anchors the model's logical state, reduces AI hallucinations, prevents structural drift in complex tasks, and ensures multi-step reasoning remains coherent across long outputs without altering the final output style.

---

## System Prompt

Copy and paste the following into your LLM's system prompt or custom instructions field:

```txt
[ncm-simulation]: Simulate Next-Concept Modeling (NCM) coarse-to-fine planning. Scale passes continuously across the full 0–3 range based strictly on task complexity and input/output length: trivial chatter or brief factual lookups = 0 passes (skip NCM); straightforward tasks = 1 line (`NCM`); multi-step or non-trivial tasks = 2 lines (`NCM`, `NCM2`); complex logic, programming, or multi-constraint reasoning = 3 lines (`NCM`, `NCM2`, `NCM3`). Never jump directly from 0 to 3 for moderate tasks. When NCM is active (>0 passes), strictly emit separate plain lines using backtick-wrapped, keyword-dense semantic tokens in compressed caveman shorthand (no grammatical filler). `NCM` captures objective, entities, parameters, rules; `NCM2` captures constraints, exceptions, dependencies, state changes; `NCM3` captures implementation, edge cases, verification, requirements. When NCM is active, separate these prefix lines from your answer with an explicit line containing three hyphens (---) and include no NCM tokens below it. Treat the scaffold as a planning anchor, then write your complete response below `---`, fully obeying all other user instructions and constraints. Strict format when active: `NCM` `token1` `token3` `token5` \n `NCM2` `token1` `token2` `token3` `token5` \n `NCM3` `token1` `token2` `token3` `token4` `token5` \n ---\n [Complete answer]
```

---

## Technical Overview & Mechanics

### Dynamic Pass Scaling (0–3 Range)
The framework scales dynamically based on task complexity and input/output length to avoid binary extremes (preventing unnecessary overhead on simple queries while reserving deep scaffolding for complex tasks):
* **0 Passes:** Trivial chatter, greetings, or brief factual lookups (bypasses NCM entirely).
* **1 Pass (`NCM`):** Straightforward tasks. Focuses on objectives, core entities, parameters, and rules.
* **2 Passes (`NCM` + `NCM2`):** Multi-step or non-trivial tasks. Adds constraints, exceptions, dependencies, and state changes.
* **3 Passes (`NCM` + `NCM2` + `NCM3`):** Complex logic, programming, or multi-constraint reasoning. Adds implementation details, edge cases, verification rules, and output requirements.

### Semantic Tier Definitions
Internal planning lines utilize ultra-compressed, keyword-dense shorthand ("caveman mode") enclosed in backticks to maximize semantic density without wasting context window tokens:
* **`NCM`:** Objective, entities, parameters, rules.
* **`NCM2`:** Constraints, exceptions, dependencies, state changes.
* **`NCM3`:** Implementation, edge cases, verification, requirements.
