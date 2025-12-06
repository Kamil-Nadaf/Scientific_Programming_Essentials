# 🤝 Contributing to AI_Assisted_Learning

Welcome!
This repository supports collaborative learning and research in **computational astrophysics** using **Python**, **statistics**, and **AI-assisted techniques**.
Whether you’re fixing typos, optimizing code, or adding new analysis notebooks, your contributions are valuable.

---

## 🧭 Repository Goals

* Build a reproducible, open-source learning pipeline.
* Encourage best practices in code, version control, and scientific documentation.
* Demonstrate collaborative research workflows with real astronomical data.

---

## 🧰 Getting Started

1. **Fork the repository**

   ```bash
   git fork https://github.com/<your-username>/AI_Assisted_Learning.git
   ```

2. **Clone your fork**

   ```bash
   git clone https://github.com/<your-username>/AI_Assisted_Learning.git
   cd AI_Assisted_Learning
   ```

3. **Create a branch**

   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Install dependencies**
   Use `requirements.txt` or `environment.yml` once available:

   ```bash
   pip install -r requirements.txt
   ```

---

## 🧠 Code Guidelines

* Follow **PEP 8** style.
* Write clear, modular, and documented functions.
* Use **docstrings** for every function and class.
* Include **AI prompt examples** where relevant (ChatGPT, Copilot, Gemini).
* Use **Markdown cells** for theory and explanations in Jupyter notebooks.

---

## 🧩 Notebook Standards

Each notebook should include:

1. **Objectives**
2. **Setup and Imports**
3. **Theory Summary**
4. **Guided Exercises (with code cells)**
5. **AI Prompt Examples**
6. **Quiz (answers hidden)**
7. **Project Task**
8. **Commit & Publish Instructions**

---

## 🔄 Git Commit Rules

Use descriptive commit messages following this structure:

```
<type>: <short summary>

Example:
feat: add Bayesian fitting example using emcee
fix: correct axis labels in Gaia plot
docs: update README for Week 4
```

Commit types: `feat`, `fix`, `refactor`, `docs`, `test`, `data`.

---

## 🧪 Continuous Integration

All notebooks are automatically checked for:

* Execution errors
* Missing dependencies
* Reproducibility consistency

To test locally before pushing:

```bash
pytest --nbval notebooks/
```

---

## 🌐 Publishing

Once your update passes all tests:

```bash
git push origin feature/your-feature-name
```

Then open a **Pull Request** with:

* A clear summary of changes
* Links to any related issues
* Screenshots or plots if relevant

---

## 💡 AI Collaboration Notes

* Use AI tools to **refactor, debug, and optimize** code, but ensure outputs are verified.
* Cite AI assistance in Markdown cells where appropriate (e.g., “Generated with help from Copilot”).

---

## 🏁 Attribution

By contributing, you agree that your work will be released under the **MIT License** (see below).

Thank you for making **AI-Assisted Learning** better with every commit!
