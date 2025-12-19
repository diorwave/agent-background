# agent-playground

A minimal playground to **run, score, and compare AI agent outputs locally**.

This project is intentionally small and explicit.
It is designed to be read, understood, and modified without learning a framework.

---

## Why this exists

When experimenting with AI agents, I often want to answer simple questions:

* How do different agents respond to the same task?
* How do their outputs compare under the same scoring logic?
* Can I test this **without** setting up a platform or framework?

Most existing tools are powerful, but heavy.
**agent-playground** focuses on the smallest possible surface area to explore these questions.

---

## What this project is

* A **local sandbox** for experimenting with agent behavior
* A way to **compare multiple agent outputs side by side**
* A place to **plug in your own scoring logic**
* A teaching tool for understanding agent evaluation

---

## What this project is NOT

This is intentionally **not**:

* ❌ a production agent framework
* ❌ an orchestration engine
* ❌ a workflow system
* ❌ a benchmarking platform
* ❌ an LLM SDK

There is no UI, no config files, no plugins, and no magic.

---

## Core idea

The core flow is simple:

```
task → agents → outputs → scores → comparison
```

You define:

1. A task
2. A list of agents (functions)
3. A scoring function

The playground runs everything and shows you the results.

---

## Basic example

```python
from agent_playground import run

def agent_a(task: str) -> str:
    return "Short answer"

def agent_b(task: str) -> str:
    return "A longer and more detailed answer"

def score(output: str) -> float:
    return min(len(output) / 50, 1.0)

results = run(
    task="Explain recursion",
    agents=[agent_a, agent_b],
    scorer=score
)

for r in results:
    print(r)
```

Example output:

```text
Agent: agent_a | Score: 0.32 | Output: Short answer
Agent: agent_b | Score: 0.88 | Output: A longer and more detailed answer
```

---

## How agents work

An **agent** is just a function:

```python
def agent(task: str) -> str:
    ...
```

* Input: the task (string)
* Output: a response (string)

No base classes. No decorators. No lifecycle hooks.

---

## How scoring works

A **scorer** is also just a function:

```python
def scorer(output: str) -> float:
    ...
```

* Input: agent output
* Output: a numeric score (e.g. 0.0–1.0)

You decide what “good” means.

---

## Design principles

* **Explicit over clever**
* **Readable over abstract**
* **Local over distributed**
* **Deterministic over realistic**

If you can’t understand the core logic in a few minutes, the project has failed its goal.

---

## Who is this for?

* People experimenting with AI agents
* Engineers who want to compare agent behaviors quickly
* Students learning how agent evaluation works
* Anyone who prefers small tools over large frameworks

---

## Roadmap (intentionally small)

Possible future ideas (not promises):

* Optional concurrent execution
* Execution timing
* Multiple scoring functions

Each addition should preserve the core simplicity.

---

## License

MIT

---

## Final note

This project is small by design.

If you’re looking for a full-featured agent platform, this is not it.
If you want something you can fully understand, fork, and bend to your needs — welcome 🙂