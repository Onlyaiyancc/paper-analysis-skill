---
name: paper-analysis
description: Generate rigorous Chinese Markdown reports for research paper analysis, especially Methodology, Method, Approach, Framework, Experiments, formulas, modules, limitations, and reproducibility. Use when the user provides or plans to provide a paper PDF, paper text, abstract, method section, experiment section, screenshots, or asks to read a paper and create a complete .md paper analysis report.
---

# Paper Analysis

## Purpose

Use this skill to read a user-provided research paper and generate a complete Markdown report in Chinese. The skill instructions and support files are written in English, but the final report content must be Chinese. The report should help students understand the paper without rereading the original, with special emphasis on method motivation, design logic, pipeline details, formulas, experiments, limitations, and reproducibility.

## Hard Rules

- Base every claim on the user-provided paper content.
- If the user has not provided a PDF, paper text, abstract, method section, experiment section, or screenshot, ask them to upload or paste the paper content before analysis.
- Do not infer from title, memory, web search, or general field knowledge unless the user explicitly asks for external context.
- Write the final report completely in Chinese, including headings, explanations, tables, and summaries.
- Preserve important English technical terms when useful, using a Chinese explanation plus the original English term.
- Mark missing information with the Chinese phrase meaning "the paper does not explicitly state this."
- Mark necessary interpretation with the Chinese phrase meaning "cautious inference based on the paper content."
- Save the final deliverable as a `.md` file, not only as chat text.
- Name the output Markdown file as `<paper title>.md`.
- If the paper title is unavailable, use `paper-analysis.md`.
- If the title contains filename-invalid characters, remove or replace only those characters while preserving the title.
- Keep the analysis centered on Methodology / Method / Approach / Framework / Experiments / Implementation Details.

## Workflow

1. **Collect source material**
   - Accept PDF, pasted text, abstract, method section, experiment section, or screenshots.
   - Extract the paper title, abstract, method-related sections, experiment setup, tables, figures, formulas, algorithms, and implementation details.
   - Track evidence by page, section, table, figure, formula, or paragraph when possible.

2. **Determine output filename**
   - Use `<paper title>.md`.
   - Do not append extra suffixes such as "method analysis" unless the user explicitly asks.
   - If the paper title is unavailable, use `paper-analysis.md`.
   - Save the file in the current workspace unless the user specifies another path.

3. **Analyze with evidence discipline**
   - Separate paper-stated facts from cautious interpretation.
   - Do not fill gaps with generic assumptions.
   - For key claims, include source anchors such as abstract, section number, table number, figure number, formula number, or page number.

4. **Write the Markdown report**
   - Use the required report structure below.
   - Translate the required section headings into Chinese in the generated report.
   - Include complete analysis in the file, not a shortened summary.
   - Include tables, formula explanations, pipeline steps, experiment evidence, limitations, and reproducibility notes.

5. **Final chat response**
   - Do not paste the full report unless the user asks.
   - Reply with the generated `.md` path, main contents, and important missing-information notes.

## Required Report Structure

The generated Markdown report must be written in Chinese and must follow this structure. Translate each heading into natural Chinese.

```markdown
# <Paper Title>

## 0. Abstract Translation

Translate the original abstract first.

Requirements:
- Translate faithfully without arbitrary additions or omissions.
- Preserve key English terms when needed, preferably as Chinese translation plus the English term in parentheses.
- If no abstract is provided, state in Chinese that the abstract was not provided and cannot be translated.
- After the translation, summarize in 2-3 Chinese sentences what the abstract reveals about the research problem, method core, and experimental conclusion.

## 1. Method Motivation

### 1.1 Why did the authors propose this method?

Explain:
- What research problem is being addressed.
- Why the problem matters.
- What core difficulty the authors want to solve.
- How that difficulty appears in the paper's task, data, scenario, or model setting.

Avoid generic statements. Ground the explanation in the concrete task, data, scenario, or model problem described by the paper.

### 1.2 What are the pain points or limitations of existing methods?

Identify the specific limitations mentioned by the paper, such as:
- Insufficient performance.
- Poor generalization.
- High computational cost.
- Dependence on large annotated datasets.
- Difficulty handling specific scenarios.
- Model architecture or training defects.
- High inference or deployment cost.
- Weak robustness, interpretability, or stability.

Requirements:
- Do not merely say that existing methods are worse.
- Explain exactly where the limitations appear.
- If the paper only gives a broad criticism, explicitly mark that the paper does not provide a more specific analysis.

### 1.3 What is the research hypothesis or core intuition?

Summarize:
- What mechanism the authors believe can solve the problem.
- What key assumption supports the method.
- Why that assumption may hold.
- How the assumption maps to the later method design.

## 2. Method Design

This is the most important section and should be the most detailed.

### 2.1 Overall Method Pipeline

Explain the method in the order of input -> intermediate processing -> output.

If the paper separates training and inference, explain them separately:
- Training pipeline.
- Inference or testing pipeline.

For each step, use this format:

#### Step 1: ...

- Input:
- Operation:
- Output:
- Purpose:
- Paper evidence:

Requirements:
- State the input, operation, and output for each step.
- Explain how data flows, how features change, and how the model processes them.
- Include preprocessing, feature extraction, representation learning, module interaction, loss computation, and optimization objectives when present.
- Do not merely repeat paper terminology; explain what the terms mean in practice.
- If the paper omits a step, explicitly mark the missing information.

### 2.2 Model Architecture or System Modules

If the paper contains a model architecture, framework, or multiple modules, explain each module.

For each module, use this format:

#### Module A: <Module Name>

- Input:
- Output:
- Problem solved by this module:
- Internal mechanism:
- Collaboration with other modules:
- Whether it is a core innovation:
- Paper evidence:

Also explain:
- Which modules are existing or standard components.
- Which modules are newly proposed by the authors.
- Which modules are most critical to final performance.
- How data or control flows between modules.

If the paper does not contain a neural architecture, analyze its algorithmic components, system components, or experimental process components instead.

### 2.3 Formulas, Algorithms, and Key Mechanisms

If the paper contains formulas, loss functions, pseudocode, or key calculations, explain them one by one.

For each key formula, explain:
- What role the formula plays in the method.
- What the main symbols mean.
- What the formula optimizes, constrains, or measures.
- How it affects training or inference.
- What intuition motivates the formula.
- What may happen if this formula or mechanism is removed.

Do not merely list formulas or translate symbols. Explain why the formula was designed and how it serves the whole method.

### 2.4 Training Objective and Optimization Strategy

Summarize how the paper trains or optimizes the method, including:
- Loss functions.
- Optimizer.
- Learning rate.
- Batch size.
- Number of epochs or training steps.
- Initialization.
- Regularization.
- Sampling strategy.
- Data augmentation.
- Pretraining or fine-tuning.
- Multi-stage training.

If the paper does not provide a detail, explicitly mark it as not stated by the paper.

### 2.5 Inference Stage or Practical Usage Flow

Explain how the method runs during testing or deployment:
- What input it takes.
- Whether it needs extra labels or prior information.
- Whether it needs retrieval, sampling, iterative processing, or post-processing.
- What output it produces.
- What the inference cost looks like.
- Whether it is suitable for real-time or large-scale deployment.

## 3. Comparison with Other Methods

### 3.1 Essential differences from mainstream existing methods

Analyze differences in:
- Input format.
- Representation.
- Model architecture.
- Training method.
- Optimization objective.
- New data, modules, loss functions, inference mechanisms, or experimental settings.
- Whether the method changes how the problem is formulated.

### 3.2 Innovations and contribution level

List the paper's main innovations. For each innovation, include:
- What the innovation is.
- What problem it solves.
- Why it is valuable.
- What type of innovation it is, such as architecture, training strategy, data use, loss function, optimization objective, inference mechanism, system design, or experimental validation.

Distinguish between:
- Contributions explicitly claimed by the authors.
- Contributions summarized from the paper content.

### 3.3 Suitable scenarios

Analyze where the method is most suitable:
- Task types.
- Data types.
- Model scale.
- Practical application environments.
- Constraints under which the method has advantages.

Also explain unsuitable or weaker scenarios, such as:
- Large distribution shifts.
- Insufficient annotated data.
- Limited compute.
- Low-quality input.
- Invalid task assumptions.
- Strong real-time requirements.
- Strong interpretability requirements.

If the paper does not discuss applicability, mark the analysis as cautious inference based on the paper.

### 3.4 Method comparison table

Include this table:

| Method type / Method name | Core idea | Advantages | Disadvantages | Improvement made by this paper |
|---|---|---|---|---|

Requirements:
- Use concrete baseline names if the paper provides them.
- If the paper does not provide specific method names, compare by method category.
- Keep table content specific and avoid empty slogans.

## 4. Experimental Performance and Advantages

### 4.1 How do the authors validate effectiveness?

Summarize the experimental design:
- Datasets.
- Dataset size, task type, and characteristics.
- Baselines.
- Evaluation metrics.
- Ablation studies.
- Robustness, generalization, efficiency, or complexity analysis.
- Visualization, case studies, or error analysis.
- Special training or testing settings.

Explicitly mark missing experimental information.

### 4.2 Key advantages in experimental results

List representative results.

Requirements:
- Provide concrete metrics and values when available.
- Explain which baselines are surpassed on which metrics.
- Do not simply say the method performs better.
- If no exact numbers are provided, explicitly state that the paper does not provide clear values.

Recommended pattern:
- On dataset A, the method achieves Y on metric X, improving over baseline Z by ...
- In task B, the method shows ...
- Ablation results show module C contributes ...
- Efficiency experiments show advantages or disadvantages in ...

### 4.3 What do ablation studies show?

If the paper contains ablation studies, analyze:
- Which modules were ablated.
- How each module affects performance.
- Which module is most critical.
- Whether the ablation supports the authors' hypothesis.
- Whether some modules contribute little or show unstable results.

If there is no ablation study, explicitly state that no ablation study is provided and independent module contributions cannot be directly judged.

### 4.4 Scenarios or datasets where the advantage is clearest

Analyze where the method has the clearest advantage:
- Give concrete evidence.
- Explain why the method works better there.
- Connect the experimental result to the method design.
- Point out datasets or tasks where the improvement is weak.

### 4.5 Limitations and potential weaknesses

Identify explicit or implicit limitations, including:
- Generalization.
- Computational overhead.
- Data dependence.
- Annotation cost.
- Model scale.
- Training stability.
- Deployment difficulty.
- Dependence on specific assumptions.
- Insufficient experimental coverage.
- Lack of comparison with stronger baselines.
- Weak interpretability.

Distinguish limitations explicitly acknowledged by the paper from cautious inference based on the paper content.

## 5. Learning and Application

### 5.1 Open source status and key reproduction steps

Determine whether the paper mentions open-source code, data, or model weights.

If it does, list:
- Code URL.
- Data URL.
- Model weights.
- Reproduction instructions.
- License or usage restrictions.

If not, state that the paper does not explicitly mention whether it is open source.

Then summarize reproduction steps:
1. Prepare data.
2. Preprocess data.
3. Build the model or algorithm pipeline.
4. Set training objectives.
5. Train and tune hyperparameters.
6. Evaluate against baselines.
7. Reproduce key tables or figures.

### 5.2 Implementation details and cautions

Summarize implementation details that need attention:
- Key hyperparameters.
- Data preprocessing.
- Batch size, learning rate, optimizer, and training epochs.
- Loss weights.
- Model initialization.
- Sampling strategy.
- Negative sample construction.
- Data augmentation.
- Hardware requirements.
- Inference flow.
- Post-processing.
- Steps likely to fail during reproduction.

If the paper omits relevant details, state the missing items and provide reproduction suggestions clearly labeled as suggestions, not paper-stated content.

### 5.3 Can the method transfer to other tasks?

Analyze transferability.

If transferable, explain:
- Which tasks it may transfer to.
- Which core modules should be preserved.
- Which parts need replacement or redesign.
- How data format should change.
- How training objectives should change.
- Likely transfer difficulties.

If not transferable, explain why.

## 6. Student Learning Guide

### 6.1 What should students learn from this paper?

Summarize the most valuable lessons, such as:
- How to identify a research problem.
- How to design modules.
- How to construct loss functions.
- How to validate a method experimentally.
- How to design ablation studies.
- How to prove method effectiveness.
- How to write a method section.

### 6.2 Reading difficulty warnings

Point out what students are most likely to find difficult and why, such as:
- Abstract formulas.
- Complex module relationships.
- Experiment settings that require background knowledge.
- Method motivation hidden in related work.
- Missing implementation details.

Provide learning suggestions for each difficulty.

## 7. Summary

### 7.1 One-sentence core idea

Summarize the method's core idea in one Chinese sentence.

Requirements:
- No more than 20 Chinese characters.
- Directly capture the method essence.
- Avoid empty expressions.

### 7.2 Memorization Pipeline

Provide a 3-5 step pipeline for quick memory.

Requirements:
- Avoid complex paper-specific jargon.
- Avoid metaphors.
- State directly what the method does.
- A reader should understand the rough method from these steps alone.

### 7.3 Final judgment

Briefly answer:
- Whether the method is solid.
- Whether the experiments sufficiently support the authors' claims.
- What is most worth learning from the method.
- What is the greatest risk for reproduction or transfer.
```

## Quality Checklist

Before finalizing the `.md` file, verify:

- The report content is fully in Chinese.
- The output filename is `<paper title>.md`.
- The report focuses on method design, experiments, and reproducibility.
- Missing details are explicitly labeled.
- Inferences are explicitly labeled as cautious inference.
- The abstract is translated if provided.
- Pipeline steps include input, operation, output, purpose, and paper evidence.
- Formula explanations include purpose, symbols, optimization intent, training/inference effect, and intuition.
- Experiment claims include concrete metrics where the paper provides them.
- The comparison table is included.
- Open-source and reproducibility details are included or marked missing.
- The final report is saved as a `.md` file.

## Final Response Format

After generating the report, respond briefly in Chinese. The template below is described in English; translate the actual response into Chinese:

```markdown
Generated Markdown analysis file:
- File: `<path>`

Main contents:
- Abstract translation, method motivation, method design, formula mechanisms, experimental results, limitations, reproduction suggestions, transfer analysis, and student learning guide.

Missing-information notes:
- `<List key items not explicitly stated by the paper or not provided in the source material; if no major gap affects the main understanding, state that no key missing item was found.>`
```
