---
name: paper-analysis
description: Generate rigorous Chinese Markdown files for research paper analysis, especially Methodology, Method, Approach, Framework, Experiments, formulas, modules, limitations, and reproducibility. Use when the user provides or plans to provide a paper PDF, paper text, abstract, method section, experiment section, screenshots, or asks to read a paper and create a complete .md paper analysis report.
---

# Paper Analysis

## Purpose

Use this skill to read a user-provided research paper and generate a complete Chinese Markdown report. The report must help students understand the paper without rereading the original, with special emphasis on method motivation, design logic, pipeline details, formulas, experiments, limitations, and reproducibility.

## Hard Rules

- Base every claim on the user-provided paper content.
- If the user has not provided a PDF, paper text, abstract, method section, experiment section, or screenshot, ask them to upload or paste the paper content before analysis.
- Do not infer from title, memory, web search, or general field knowledge unless the user explicitly asks for external context.
- Mark missing information as `论文未明确说明`.
- Mark necessary interpretation as `基于论文内容的谨慎推断`.
- Write the final report completely in Chinese.
- Save the final deliverable as a `.md` file, not only as chat text.
- Name the output Markdown file exactly as `论文标题.md`.
- If the paper title is unavailable, use `论文方法分析.md`.
- If the title contains filename-invalid characters, remove or replace only those characters while preserving the title.
- Keep the analysis centered on Methodology / Method / Approach / Framework / Experiments / Implementation Details.

## Workflow

1. **Collect source material**
   - Accept PDF, pasted text, abstract, method section, experiment section, or screenshots.
   - Extract the paper title, abstract, method-related sections, experiment setup, tables, figures, formulas, algorithms, and implementation details.
   - Track evidence by page, section, table, figure, formula, or paragraph when possible.

2. **Determine output filename**
   - Use `论文标题.md`.
   - Do not append `方法深度分析` or any other suffix unless the user explicitly asks.
   - If the paper title is unavailable, use `论文方法分析.md`.
   - Save the file in the current workspace unless the user specifies another path.

3. **Analyze with evidence discipline**
   - Separate paper-stated facts from cautious interpretation.
   - Do not fill gaps with generic assumptions.
   - For key claims, include source anchors such as `摘要`, `第 3.1 节`, `表 2`, `图 4`, `公式 (3)`, or `第 X 页`.

4. **Write the Markdown report**
   - Use the required structure below.
   - Include complete analysis in the file, not a shortened summary.
   - Include tables, formula explanations, pipeline steps, experiment evidence, limitations, and reproducibility notes.

5. **Final chat response**
   - Do not paste the full report unless the user asks.
   - Reply with the generated `.md` path, main contents, and important missing-information notes.

## Required Report Structure

```markdown
# 论文标题

## 0. 摘要翻译

请先翻译论文摘要原文。

要求：
- 忠实翻译，不随意增删。
- 保留关键术语英文原词，可采用“中文翻译（English term）”形式。
- 如果用户没有提供摘要，请说明：**“未提供摘要，无法翻译。”**
- 翻译后，用 2-3 句话概括摘要中透露的研究问题、方法核心和实验结论。

## 1. 方法动机

### 1.1 作者为什么提出这个方法？

解释：
- 研究问题是什么；
- 该问题为什么重要；
- 作者希望解决什么核心困难；
- 该困难在论文任务或应用场景中具体体现在哪里。

避免空泛表述，要结合论文中的具体任务、数据、场景或模型问题说明。

### 1.2 现有方法的痛点或不足是什么？

具体指出论文中提到的已有方法局限，例如：
- 性能不足；
- 泛化能力差；
- 计算成本高；
- 依赖大量标注数据；
- 难以处理特定场景；
- 模型结构或训练方式存在缺陷；
- 推理效率或部署成本较高；
- 鲁棒性、可解释性或稳定性不足。

要求：
- 不要只写“现有方法效果不好”。
- 必须说明“不足具体体现在哪里”。
- 如果论文只笼统批评现有方法，标注：**“论文未给出更具体分析。”**

### 1.3 论文的研究假设或核心直觉是什么？

概括：
- 作者认为通过什么机制可以解决问题；
- 方法背后的关键假设是什么；
- 这个假设为什么可能成立；
- 该假设与后续方法设计之间有什么对应关系。

## 2. 方法设计

这是最重要的部分，必须写得最细致。

### 2.1 方法整体流程 Pipeline

按照“输入 -> 中间处理 -> 输出”的顺序解释方法流程。

如果论文区分训练阶段和推理阶段，请分开说明：
- 训练阶段 pipeline；
- 推理/测试阶段 pipeline。

每一步使用以下格式：

#### 步骤 1：……

- 输入：
- 操作：
- 输出：
- 作用：
- 对应论文位置：

要求：
- 每一步都说明输入、操作、输出。
- 讲清楚数据如何流动、特征如何变化、模型如何处理。
- 如果有数据预处理、特征提取、表示学习、模块交互、损失计算、优化目标，也要纳入流程。
- 不要只复述论文术语，要解释术语背后的实际含义。
- 如果论文没有完整说明某一步，明确标注缺失。

### 2.2 模型结构或系统模块

如果论文涉及模型结构、框架或多个模块，请逐一说明。

每个模块按以下格式分析：

#### 模块 A：模块名称

- 输入：
- 输出：
- 该模块解决的问题：
- 模块内部如何工作：
- 与其他模块如何协同：
- 是否属于核心创新：
- 论文依据：

特别说明：
- 哪些模块是已有模型或标准组件；
- 哪些模块是作者新提出的；
- 哪些模块对最终性能最关键；
- 模块之间的数据流或控制流关系。

如果论文没有神经网络模型结构，改为分析算法组件、系统组件或实验流程组件。

### 2.3 公式、算法与关键机制解释

如果论文中包含公式、损失函数、算法伪代码或关键计算过程，请逐一解释。

每个关键公式说明：
- 公式在方法中起什么作用；
- 每个主要符号代表什么；
- 公式想优化、约束或衡量什么；
- 它如何影响模型训练或推理；
- 设计这个公式的直觉是什么；
- 如果去掉该公式或机制，可能会带来什么问题。

不要只罗列公式或翻译符号，必须解释设计原因及其如何服务整体方法。

### 2.4 训练目标与优化策略

总结论文如何训练模型或优化方法，包括：
- 损失函数；
- 优化器；
- 学习率；
- batch size；
- 训练轮数；
- 初始化方式；
- 正则化策略；
- 采样策略；
- 数据增强；
- 预训练或微调方式；
- 多阶段训练流程。

如果论文未提供相关细节，明确写：**“论文未明确说明。”**

### 2.5 推理阶段或实际使用流程

说明方法在测试或实际应用时如何运行：
- 输入什么；
- 是否需要额外标注或先验信息；
- 是否需要检索、采样、多轮迭代或后处理；
- 输出结果是什么；
- 推理成本如何；
- 是否适合实时或大规模部署。

## 3. 与其他方法对比

### 3.1 与现有主流方法的本质区别

说明本文方法与已有方法相比的核心区别：
- 输入形式是否不同；
- 表示方式是否不同；
- 模型结构是否不同；
- 训练方式是否不同；
- 优化目标是否不同；
- 是否引入新的数据、模块、损失函数、推理机制或实验设置；
- 是否改变了问题建模方式。

### 3.2 创新点与贡献度

列出论文主要创新点。每个创新点包括：
- 创新内容是什么；
- 解决了什么问题；
- 为什么有价值；
- 属于哪类创新：
  - 方法结构创新；
  - 训练策略创新；
  - 数据使用创新；
  - 损失函数或优化目标创新；
  - 推理机制创新；
  - 系统设计创新；
  - 实验验证创新。

区分：
- 作者明确声称的贡献；
- 基于论文内容总结出的贡献。

### 3.3 适用场景

分析该方法更适合哪些场景：
- 哪类任务；
- 哪类数据；
- 哪类模型规模；
- 哪些实际应用环境；
- 在什么限制条件下更有优势。

同时说明不适合或可能效果不佳的场景，例如：
- 数据分布变化较大；
- 标注数据不足；
- 算力受限；
- 输入质量较差；
- 任务假设不成立；
- 需要强实时性；
- 需要高可解释性。

如果论文没有讨论适用范围，标注：**“基于论文内容的谨慎推断。”**

### 3.4 方法对比表

| 方法类型/方法名称 | 核心思想 | 优点 | 缺点 | 本文方法的改进点 |
|---|---|---|---|---|

要求：
- 如果论文给出具体 baseline 名称，请使用具体名称。
- 如果论文没有给出具体方法名称，可按方法类别进行对比。
- 表格内容要具体，不要写成空泛口号。

## 4. 实验表现与优势

### 4.1 作者如何验证方法有效性？

总结实验设计，包括：
- 使用了哪些数据集；
- 数据集规模、任务类型和特点；
- 对比了哪些 baseline；
- 使用了哪些评价指标；
- 是否有消融实验；
- 是否有鲁棒性、泛化性、效率或复杂度分析；
- 是否有可视化分析、案例分析或错误分析；
- 训练和测试设置是否有特殊之处。

如果论文没有提供某些实验信息，请明确标注缺失。

### 4.2 实验结果中的关键优势

列出最具代表性的实验结果。

要求：
- 尽量给出具体指标和数值；
- 说明在哪些指标上超过了哪些 baseline；
- 不要只说“效果更好”；
- 如果论文没有提供明确数值，说明：**“论文未提供明确数值。”**

推荐格式：
- 在数据集 A 上，本文方法在指标 X 上达到 Y，相比 baseline Z 提升了……
- 在任务 B 中，本文方法表现出……
- 消融实验表明，模块 C 带来了……
- 效率实验表明，本文方法在……方面具有优势/不足。

### 4.3 消融实验说明了什么？

如果论文包含消融实验，请重点分析：
- 消融了哪些模块；
- 每个模块对性能的影响；
- 哪个模块最关键；
- 消融结果是否支持作者的方法假设；
- 是否存在某些模块贡献不明显或结果不稳定。

如果没有消融实验，写：**“论文未提供消融实验，因此无法直接判断各模块独立贡献。”**

### 4.4 优势最明显的场景或数据集

分析在哪些场景、数据集或任务下，该方法优势最明显。

要求：
- 给出具体证据；
- 说明为什么在这些场景下更有效；
- 结合方法设计解释实验结果；
- 如果某些数据集上提升不明显，也要指出。

### 4.5 局限性与潜在不足

指出论文中明确承认或隐含的不足，包括但不限于：
- 泛化能力；
- 计算开销；
- 数据依赖；
- 标注成本；
- 模型规模；
- 训练稳定性；
- 实际部署难度；
- 对特定假设的依赖；
- 实验覆盖不足；
- 与更强 baseline 对比不足；
- 可解释性不足。

区分“论文明确承认的局限”和“基于论文内容的谨慎推断”。

## 5. 学习与应用

### 5.1 是否开源与复现关键步骤

判断论文是否提到代码、数据或模型开源。

如果论文提到开源信息，请列出：
- 代码地址；
- 数据地址；
- 模型权重；
- 复现说明；
- 许可证或使用限制。

如果论文未提到，写：**“论文未明确说明是否开源。”**

然后总结复现该方法的关键步骤：
1. 准备数据；
2. 数据预处理；
3. 搭建模型或算法流程；
4. 设置训练目标；
5. 训练与调参；
6. 评估与 baseline 对比；
7. 复现实验表格或关键图像。

### 5.2 实现细节与注意事项

总结实现该方法时需要特别注意的内容，例如：
- 关键超参数；
- 数据预处理方式；
- batch size、学习率、优化器、训练轮数；
- 损失函数权重；
- 模型初始化；
- 采样策略；
- 负样本构造；
- 数据增强；
- 硬件需求；
- 推理流程；
- 后处理方式；
- 容易复现失败的环节。

如果论文未提供相关细节，请说明缺失项，并给出合理复现建议，但必须标注为：**“复现建议，非论文明确内容。”**

### 5.3 是否可以迁移到其他任务？

分析该方法是否可以迁移到其他任务。

如果可以，请说明：
- 可以迁移到哪些任务；
- 需要保留哪些核心模块；
- 哪些部分需要替换或重新设计；
- 数据格式需要如何调整；
- 训练目标需要如何调整；
- 迁移时最可能遇到的困难。

如果不适合迁移，也请说明原因。

## 6. 学生学习指南

### 6.1 读这篇论文最应该学什么？

总结学生最值得学习的内容，例如：
- 如何发现问题；
- 如何设计模块；
- 如何构造损失函数；
- 如何做实验验证；
- 如何设计消融实验；
- 如何证明方法有效；
- 如何写方法部分。

### 6.2 阅读难点提醒

指出学生最容易读不懂的地方，并解释原因，例如：
- 公式较抽象；
- 模块之间关系复杂；
- 实验设置依赖背景知识；
- 方法动机隐藏在相关工作中；
- 论文省略了实现细节。

给出对应学习建议。

## 7. 总结

### 7.1 一句话概括核心思想

用一句话概括该方法的核心思想。

要求：
- 不超过 20 个汉字；
- 直击方法本质；
- 不使用空泛表达。

### 7.2 速记版 Pipeline

给出一个 3-5 步速记版 pipeline。

要求：
- 不使用论文中的复杂专业术语；
- 不使用比喻；
- 直白说明方法做了什么；
- 读者只看这几步，也能大体理解论文方法。

格式：
1. 输入原始数据
2. 提取关键信息
3. 组合并筛选有效特征
4. 训练模型完成预测
5. 根据结果评估改进效果

### 7.3 最终判断

用简短段落回答：
- 这篇论文的方法是否扎实；
- 实验是否充分支撑作者结论；
- 方法最值得借鉴的地方是什么；
- 复现或迁移时最大的风险是什么。
```

## Quality Checklist

Before finalizing the `.md` file, verify:

- The report is fully in Chinese.
- The output filename is `论文标题.md`.
- The report focuses on method design, experiments, and reproducibility.
- Missing details are explicitly labeled.
- Inferences are explicitly labeled as cautious inference.
- The abstract is translated if provided.
- Pipeline steps include input, operation, output, role, and paper evidence.
- Formula explanations include purpose, symbols, optimization intent, training/inference effect, and intuition.
- Experiment claims include concrete metrics where the paper provides them.
- The comparison table is included.
- Open-source and reproducibility details are included or marked missing.
- The final report is saved as a `.md` file.

## Final Response Format

After generating the report, respond briefly:

```markdown
已生成 Markdown 分析文件：
- 文件：`<path>`

主要内容：
- 摘要翻译、方法动机、方法设计、公式机制、实验结果、局限性、复现建议、迁移分析和学习指南。

信息缺失说明：
- `<列出论文未明确说明或材料未提供的关键项；如果没有明显缺失，写“未发现影响主线理解的关键缺失项”。>`
```
