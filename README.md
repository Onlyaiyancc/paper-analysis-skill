# Paper Analysis Skill

`paper-analysis` is a Codex skill for generating rigorous Chinese Markdown reports from research papers. It is designed for students who want to understand a paper's methodology, framework, experiments, limitations, and reproducibility path without rereading the original paper.

## What It Does

- Reads a user-provided paper PDF, paper text, abstract, method section, experiment section, or screenshots.
- Produces a complete Chinese `.md` report named after the paper title.
- Focuses on Methodology, Method, Approach, Framework, Experiments, formulas, modules, limitations, and reproducibility.
- Requires evidence-based analysis and explicitly labels missing details in Chinese.
- Separates cautious interpretation from paper-stated facts.

## Install

Copy the skill folder into your Codex skills directory:

```powershell
Copy-Item -Recurse -Force .\.agents\skills\paper-analysis "$env:USERPROFILE\.codex\skills\paper-analysis"
```

Or use it as a project-local skill by keeping this repository's `.agents/skills/paper-analysis` folder in your project.

## Usage

After installing, ask Codex:

```text
Use $paper-analysis to analyze this uploaded paper and generate a complete Markdown report.
```

The generated report should be saved as:

```text
<paper-title>.md
```

## Skill Files

- `.agents/skills/paper-analysis/SKILL.md`
- `.agents/skills/paper-analysis/agents/openai.yaml`

## License

MIT
