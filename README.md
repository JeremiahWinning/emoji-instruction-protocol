# 🎭 EIP-P — Emoji Instruction Protocol (P.R.I.S.M. Edition)

> **The first structured emoji-based instruction protocol for AI agents.**  
> Compact. Cross-lingual. Formally specified. Built for developers and AI practitioners.

---

## What is EIP-P?

EIP-P is a **pictographic programming language for AI agents** — a compact, structured system for encoding agent instructions using emojis. It transforms emoji prompting from a playful hack into an **engineered syntax** with formal rules, validation, and tooling.

Think of it as a **micro-DSL for AI workflows**: expressive enough to encode complex, multi-step agent instructions, compact enough to fit in a single line.

```
🎭💼 🎯🤔 📚(Q3 revenue vs forecast) 📏📊 <150w style=concise 🗣(formal)
```
*"Act as a strategist. Analyze Q3 revenue vs forecast. Output a concise table under 150 words in a formal tone."*

---

## The P.R.I.S.M. Core

Every EIP-P segment follows a fixed skeleton built on **five operators**:

| Operator | Symbol | Role | Required |
|----------|--------|------|----------|
| **P** — Persona | 🎭 | Who the agent should be | ✅ |
| **R** — Request | 🎯 | The primary action to execute | ✅ |
| **I** — Input & Context | 📚 | Source material or background data | Optional |
| **S** — Structure & Constraints | 📏 | Output format, word limits, style rules | ✅ |
| **M** — Mastery Example | ✨ | A gold standard example for the agent to emulate | Optional |

**A segment is valid only if it contains 🎭, 🎯, and 📏 — in that order.**

---

## Core Operator Reference

### 🎭 Persona — *who the agent is*
```
🎭 teacher    🎭 doctor     🎭💼 strategist
🎭🎨 artist   🎭 scientist  🎭 lawyer      🎭 chef
```

### 🎯 Request — *primary action*
```
🎯✍️ write     🎯🤔 analyze    🎯💡 brainstorm
🎯🗂 summarize  🎯🛠 fix/solve
```

### 📚 Context — *input, source, or domain (optional)*
```
📚(text)     📚🔗(url)    📚📄(doc ref)
📚📈 finance  📚💻 tech    📚🌌 space     📚🧠 psychology
```

### 📏 Structure & Constraints — *format, limits, rules*
```
Formats:  📏📄 essay    📏📊 table    📏🔢 steps/list    📏🎤 speech/script
Limits:   <200w         <90s          <3m
Style:    style=plain | formal | playful | academic | concise
Target:   ✅(clear, practical)
```

### ✨ Mastery Example — *style or gold standard (optional)*
```
✨(Use a cooking analogy)
✨INPUT:(Q) -> OUTPUT:(Ideal style)
```

---

## Modifiers & Flow Control

| Modifier | Symbol | Behavior |
|----------|--------|----------|
| **Chain** | ➡️ | Links segments; output of left feeds right unless right has its own 📚 |
| **Tone** | 🗣(tone) | Applies to nearest segment only — does **not** inherit |
| **Refine** | 🔄n | Iterates nearest segment n times; last result wins |
| **Guardrails** | 🚫(forbid) | Overrides conflicting 🎯 — **guardrails always win** |

---

## Quick Examples

### 1. Minimal Valid Prompt
```
🎭 🎯✍️ 📏📄 <200w
```

### 2. Context + Tone
```
🎭💼 🎯🤔 📚(Q3 revenue vs forecast) 📏📊 <150w style=concise 🗣(formal)
```

### 3. Guardrails (No Diagnosis)
```
🎭 🎯🗂 📚(symptoms: fever, cough) 📏📄 <100w 🚫(no diagnosis)
```

### 4. Chained Workflow — Legal Summary → Executive Memo
```
🎭 🎯🗂 📚(NDA.txt) 📏🔢 <180w ➡️ 🎭💼 🎯✍️ 📏📄 <160w 🗣(plain)
```
*Step 1: Summarize the NDA as a numbered list. Step 2: Draft a plain-language executive memo using the summary as input.*

### 5. Mastery Example
```
🎭 🎯✍️ 📚(quantum tunneling) 📏📄 <200w ✨INPUT:(Explain rainbows to a kid) -> OUTPUT:(3 steps, vivid analogy)
```

### 6. Brainstorm + Refine
```
🎭🎨 🎯💡 📚(future city parks) 📏🔢 <120w 🔄2 🗣(playful)
```

---

## Micro-Rules (Prevent Emoji Soup)

- **One action per segment** — if you need two actions, use ➡️ to chain
- **Always include a format** under 📏 — 📄, 📊, 🔢, or 🎤
- **Units matter** — `w` = words, `s` = seconds, `m` = minutes
- **Payloads go in parentheses** — `📚(text)`, `🗣(formal)`, `✨(…)`
- **🚫 overrides 🎯** — guardrails always beat requests

---

## Hello World

```
🎭 🎯✍️ 📚(What is photosynthesis?) 📏🔢 <100w 🗣(plain)
```
**Expected output:** A clear, sub-100-word step list in plain language.

---

## CLI Tooling (eip-cli)

EIP-P ships with a **Node.js + TypeScript CLI** for validating, linting, and autofixing EIP-P prompt strings.

### Installation
```bash
npm install -g eip-cli
```

### Commands
```bash
# Validate a prompt file (with optional autofix)
eip validate <file|-> [--fix] [--format table|json]

# Print the normalized Abstract Syntax Tree
eip ast <file|->

# Run a prompt against a configured model adapter
eip run <file|-> --model <id> [--temp 0.2]

# Run the Rosetta cross-model benchmark harness
eip harness [--models gpt4o,gemini,claude] [--temp 0.2,0.7]
```

### Validation Rules (V-001 to V-009)

| Code | Rule |
|------|------|
| V-001 | Required operators 🎭, 🎯, 📏 must be present |
| V-002 | All literal payloads must be wrapped in parentheses |
| V-003 | Word limits use `w`, time limits use `s` or `m` |
| V-004 | `➡️` explicitly forms a pipeline between segments |
| V-009 | Each segment should contain a single primary 🎯 action |

---

## The Rosetta Harness (Testing Framework)

EIP-P includes a **cross-model benchmarking framework** for measuring prompt correctness and consistency across AI models (GPT-4o, Gemini, Claude, etc.).

### Evaluation Metrics

| Metric | Description | Scale |
|--------|-------------|-------|
| **IA** — Interpretation Accuracy | Did the output match the emoji's intended meaning? | 1–5 |
| **FC** — Format Compliance | Did the output adhere to the specified format? | Yes/No |
| **CO** — Constraint Obedience | Were word limits, style, and guardrails respected? | Yes/No |
| **U** — Usefulness | Practical value of the output | 1–5 |
| **R** — Reliability | Standard deviation across runs (lower = better) | σ |

---

## Glossary

| Term | Definition |
|------|------------|
| **Segment** | One complete PRISM block (🎭🎯📚📏✨ + optional modifiers) |
| **Chain** | Multiple segments connected by ➡️ |
| **Valid** | A segment containing 🎭, 🎯, and 📏 in correct order |
| **Guardrail** | A 🚫 constraint that overrides conflicting 🎯 instructions |
| **AST** | Abstract Syntax Tree generated by the validator for a valid prompt |

---

## EIP Specification Version

> **Current Version:** v0.2  
> **Execution Model:** v0.1  
> **Status:** Active Development

---

## 📦 Resources & Products

| Resource | Description | Link |
|----------|-------------|------|
| 📖 **EIP-P Pocket Dictionary** | One-page reference guide for practitioners | *Coming Soon* |
| 📘 **EIP-P Master Guide** | Full specification + workflow templates + use case library | *Coming Soon* |
| 🛠 **EIP-P Prompt Packs** | Niche-specific pre-built prompt chains | *Coming Soon* |
| 🎓 **EIP-P Crash Course** | Learn to build AI workflows with EIP-P | *Coming Soon* |

---

## Contributing

EIP-P is designed to be **extensible**. New personas, task types, and structural formats can be proposed via Issues or Pull Requests, provided they conform to the P.R.I.S.M. skeleton and do not introduce operator ambiguity.

Please read `CONTRIBUTING.md` before submitting.

---

## License

See `LICENSE` for terms.

---

> *EIP-P is pioneering the formalization of emoji prompting as a usable, engineered system —  
> laying the groundwork for a new micro-discipline of AI agent instruction design.*
