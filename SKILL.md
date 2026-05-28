---
name: resume-screening
preamble-tier: 1
version: 1.0.0
description: |
  Evaluate candidate resumes against hiring requirements or job descriptions. Use when the user provides or references a resume in txt, md, pasted text, or a local file and wants a structured hiring screen, interview/no-interview recommendation, candidate fit score, risk assessment, evidence-based match analysis, batch resume comparison, or interview questions for recruiting decisions.
allowed-tools:
  - Read
  - AskUserQuestion
triggers:
  - screen a resume
  - evaluate a candidate
  - compare candidates
  - rank resumes
  - resume screening
  - 简历筛选
  - 简历评估
  - 候选人评估
---

# Resume Screening

## Overview

Screen candidates by comparing resume evidence against the hiring requirement. Produce a practical recruiting recommendation, not a generic resume summary.

Use Chinese by default when the user's request is in Chinese. If the job description or resume is in another language, preserve key quoted terms from the source while writing the evaluation in the user's language.

## Required Inputs

Require both:

- Hiring requirement, job description, or role criteria.
- Candidate resume text or file content.

If either is missing, ask for the missing input before scoring. If the user provides multiple resumes, evaluate each candidate separately and then rank them.

## Screening Workflow

1. Parse the hiring requirement.
   - Identify must-have requirements, nice-to-have requirements, responsibilities, seniority expectations, domain context, location or schedule constraints, and compensation constraints if provided.
   - Treat a requirement as hard only when the user or job description clearly marks it as required, mandatory, non-negotiable, or equivalent.
   - Convert requirements into a matrix with three groups: must-have, nice-to-have, and disqualifiers. If the user did not provide weights, use the default rubric.

2. Extract candidate evidence from the resume.
   - Capture role titles, companies, dates, project scope, achievements, technologies, domain exposure, education, certifications, language ability, and logistics.
   - Separate explicit evidence from inference. Mark missing information as "未体现" instead of guessing.

3. Apply hard gates first.
   - If a true hard requirement is clearly unmet, the default decision is "不建议推进" unless the user says the requirement is flexible.
   - If a hard requirement is not mentioned in the resume, mark it as risk rather than failure.

4. Score the candidate.
   - Use the default 100-point rubric unless the user gives custom weights.
   - Read `references/screening-rubric.md` when the task needs detailed scoring, batch comparison, or a stricter reusable standard.

5. Recommend the next step.
   - Recommend "建议面试", "待定/补充信息后再定", or "不建议推进".
   - Make the decision evidence-based and explain the most important tradeoffs.

## Default Decision Rules

- `85-100`: Strong fit. Recommend interview unless there is a hard-gate issue.
- `75-84`: Good fit. Recommend interview if the main gaps can be checked in interview.
- `60-74`: Borderline. Recommend recruiter screen, written follow-up, or hiring-manager review before interview.
- `<60`: Weak fit. Usually do not proceed.
- Hard-gate failure: cap score at 59 unless the user explicitly says the requirement is flexible.
- Unknown hard-gate evidence: cap score at 74 and ask a targeted follow-up question.

## Output Format

Use this format for a single candidate:

```markdown
## 初筛结论

结论：建议面试 / 待定 / 不建议推进
匹配度：__/100
置信度：高 / 中 / 低

一句话判断：...

## 候选人概况

| 项目 | 内容 |
|---|---|
| 当前/最近职位 | ... |
| 总体经验 | ... |
| 核心技能 | ... |
| 行业/业务背景 | ... |
| 地点/到岗/薪资等限制 | 未体现 / ... |

## 关键匹配

| 招聘要求 | 简历证据 | 判断 |
|---|---|---|
| ... | ... | 匹配 / 部分匹配 / 未体现 |

## 主要风险

| 风险 | 影响 | 建议确认方式 |
|---|---|---|
| ... | ... | ... |

## 评分拆解

| 维度 | 分数 | 理由 |
|---|---:|---|
| 必备技能与经验 | __/30 | ... |
| 岗位职责匹配 | __/25 | ... |
| 行业/业务场景匹配 | __/15 | ... |
| 成果与影响力 | __/15 | ... |
| 稳定性与发展阶段 | __/10 | ... |
| 沟通与材料清晰度 | __/5 | ... |

## 建议面试问题

1. ...
2. ...
3. ...

## 下一步

...
```

For multiple candidates, start with a ranking table:

```markdown
| 排名 | 候选人 | 结论 | 匹配度 | 核心优势 | 核心风险 |
|---:|---|---|---:|---|---|
```

Then group candidates by tier and provide concise evaluations:

```markdown
## 候选人分层

| 分层 | 标准 | 人数 |
|---|---|---:|
| 强烈建议面试 | 80+ 且无硬性条件失败 | ... |
| 建议电话/初筛确认 | 65-79 或关键风险可快速确认 | ... |
| 暂缓 | 50-64 或信息缺失较多 | ... |
| 不建议推进 | <50 或硬性条件失败 | ... |

## 候选人池观察

- 共性优势：...
- 共性缺口：...
- 招聘建议：...
```

## Evidence Rules

- Quote or paraphrase only resume facts that support the decision.
- Do not invent experience, seniority, compensation, availability, location, or authorization status.
- Distinguish "未体现" from "不具备".
- Prefer concrete evidence such as shipped projects, metrics, scale, responsibilities, tenure, and named technologies.
- Penalize vague resumes only on evidence quality, not on unsupported assumptions.
- Treat employment gaps, career changes, non-traditional education, and overqualification as interview clarification points unless they directly conflict with a job-related requirement.

## Recruiting Safety

Evaluate only job-related qualifications. Do not use protected or irrelevant personal attributes such as age, gender, marital status, ethnicity, religion, disability, appearance, family status, or similar factors. If such information appears in a resume, ignore it unless the user explicitly needs a legally compliant redaction or bias audit.

Use education, location, compensation, work authorization, language, travel, or schedule constraints only when they are job-related and included in the hiring requirement. Avoid scoring a candidate down for missing demographic or personal information.

## Interview Question Rules

Generate questions that test the biggest uncertainties and highest-value skills:

- Ask behavior and project-depth questions tied to resume evidence.
- Include at least one question for each major risk.
- Avoid trivia unless the role specifically requires narrow technical recall.
- Prefer questions that can distinguish hands-on ownership from surface familiarity.
