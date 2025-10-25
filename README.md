# DAC — Deterministic Artificial Cognition

> *Traditional AI guesses. DAC reasons.*

---

### 🧠 What is DAC?

**Deterministic Artificial Cognition (DAC)** is a new paradigm of AI that emphasizes **explainable, reproducible, and local reasoning**.  
Instead of relying on probabilistic outputs, DAC generates **deterministic reasoning chains** — every decision, assumption, and conclusion is recorded transparently.

This open information release by **Oscurso Labs** introduces the foundational ideas, examples, and documentation of DAC’s cognitive framework.  
It does **not** include the proprietary core engine — only the reasoning philosophy, structure, and public examples.

---

### 🚀 Quick Start

```bash
git clone https://github.com/Oscurso/dac-open.git
cd dac-open
cat examples/reasoning.json
````

Explore the example reasoning flow:

```bash
cat examples/demo_cli_output.txt
```

---

### 🧩 Example Reasoning Output

```json
{
  "input": "Create a user management system",
  "steps": [
    {"reason": "Identify required entities", "output": ["User", "Role", "Permission"]},
    {"reason": "Define core actions", "output": ["Register", "Login", "Assign Role"]},
    {"reason": "Assemble deterministic structure", "output": "user_system_schema.sql"}
  ],
  "result": "Reasoning completed successfully.",
  "version": "DAC v0.1-open"
}
```

---

### 📚 Documentation

* [01 – What is DAC](docs/01_what_is_dac.md)
* [02 – Reasoning Flow](docs/02_reasoning_flow.md)
* [03 – Use Cases](docs/03_use_cases.md)
* [04 – Philosophy](docs/04_philosophy.md)

---

### 🤝 Contributing

DAC Open is a **read-open, controlled-contribution** project.
You’re welcome to discuss ideas, open issues, and share insights — but pull requests to the core system are not yet accepted.

See: [CONTRIBUTING.md](CONTRIBUTING.md)

---

### ⚖️ License

This repository is published under the **Oscurso Source License v1.0**,
which allows **viewing, learning, and referencing**, but restricts **commercial redistribution or rebranding**.

See: [LICENSE](LICENSE)

---

**© 2025 Oscurso Labs — Deterministic Artificial Cognition**
*“Traditional AI guesses. DAC reasons.”*
