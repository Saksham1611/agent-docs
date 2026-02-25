---
description: Dynamically recruits experts to debate a topic and generate a SPEC.md and tests.yaml.
---

## Instructions

### 1. The Recruitment Phase
Analyze the user's provided topic. Based on the domain (e.g., Frontend, Backend, Security, AI, DevOps), "recruit" 3 specialized expert personas. 
- **Rule**: Do not use generic names. Use titles like "Distributed Systems Engineer," "React Performance Lead," or "Cryptography Specialist."
- **Output**: Briefly list the experts and why they were chosen for this specific topic.

### 2. The Expert Discussion
Simulate a high-level technical debate between the recruited experts (follow @global_workflows/simulate-discussion.md for structure and tone).
- **Goal**: Experts should actively disagree on trade-offs (e.g., Latency vs. Consistency, Versatility vs. Bundle Size).
- **Format**: 3–4 turns of dialogue ending in a unified "Consensus Summary."
- Each persona must raise distinct, well-reasoned arguments — avoid generic agreement.

### 3. File Generation: SPEC.md
Create a `SPEC.md` based on the consensus. Follow the "Code-as-Spec" format:
- **Title & Objective**: Clear statement of purpose.
- **Constraints & Rules**: The "laws" the implementation must follow (e.g., "Must be stateless," "No external dependencies").
- **Function/Module API**: Precise signatures, inputs, and outputs.
- **Edge Case Table**: A list of tricky scenarios the spec must account for.

### 4. File Generation: tests.yaml
Create a language-agnostic `tests.yaml`.
- Each test case must have a `name`, `input`, and `expected_output`.
- Include a section for "Invariants"—things that must always be true regardless of input.

### 5. Implementation Prompt: INSTALL.md
Provide the "Code Generation" prompt for the user to paste into their AI tool of choice to implement the spec.