# Resume Screening Skill / 简历初筛 Skill

一个可复用的 AI Skill，用于根据招聘需求评估候选人简历，帮助 Claude、Codex 或其他支持 Skill 的智能体输出结构化、有证据支撑的招聘初筛建议。

A reusable AI skill for screening candidate resumes against hiring requirements. It helps Claude, Codex, or other skill-compatible agents produce structured, evidence-based recruiting recommendations.

## 功能 / What It Does

- 对比简历与岗位 JD 或招聘需求。
- 区分必备条件、加分项和淘汰条件。
- 使用可复用的 100 分评分标准评估候选人。
- 标记简历中缺失的信息、潜在风险和需要面试确认的问题。
- 生成有针对性的面试问题。
- 支持单个候选人评估和多候选人批量排名。
- 只围绕岗位相关标准进行判断，避免使用无关个人信息。

- Compares a resume with a job description or hiring requirement.
- Separates must-have requirements, nice-to-have requirements, and disqualifiers.
- Scores candidates with a reusable 100-point rubric.
- Flags missing evidence, interview risks, and follow-up points.
- Generates practical interview questions.
- Supports both single-candidate screening and batch candidate ranking.
- Keeps evaluation focused on job-related criteria.

## 目录结构 / Repository Structure

```text
.
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
|-- references/
|   `-- screening-rubric.md
`-- .gitignore
```

## 使用方式 / Usage

中文使用示例：

```text
使用 $resume-screening，根据下面的招聘需求和候选人简历，判断是否建议进入面试。

招聘需求：
...

简历：
...
```

English example:

```text
Use $resume-screening to evaluate this candidate resume against the hiring requirement and recommend whether to proceed to interview.

Hiring requirement:
...

Resume:
...
```

## 输出内容 / Output

该 Skill 会输出结构化初筛报告，包括：

- 是否建议进入面试
- 匹配度评分
- 判断置信度
- 候选人概况
- 招聘要求匹配表
- 主要风险和确认方式
- 评分拆解
- 建议面试问题
- 下一步建议

The skill produces a structured screening report with:

- interview recommendation
- fit score
- confidence level
- candidate profile
- requirements match table
- key risks and verification methods
- score breakdown
- interview questions
- next-step recommendation

如果输入多个候选人，它还会输出候选人排名、分层和候选人池观察。

For multiple candidates, it also provides a ranking table, candidate tiers, and applicant-pool insights.

## 安装 / Install

### Claude

将本仓库复制到 Claude 的 Skills 目录，或通过你使用的 Claude-compatible skills workflow 导入：

Copy this folder into your Claude skills directory, or import it through your Claude-compatible skills workflow:

```text
resume-screening/
|-- SKILL.md
|-- agents/openai.yaml
`-- references/screening-rubric.md
```

### Codex

在仓库根目录执行以下 PowerShell 命令，将 Skill 复制到 Codex skills 目录：

Run the following PowerShell commands from the repository root to copy the skill into your Codex skills directory:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills\resume-screening"
Copy-Item -Force "SKILL.md" "$env:USERPROFILE\.codex\skills\resume-screening\SKILL.md"
Copy-Item -Recurse -Force "agents" "$env:USERPROFILE\.codex\skills\resume-screening\agents"
Copy-Item -Recurse -Force "references" "$env:USERPROFILE\.codex\skills\resume-screening\references"
```

然后这样调用：

Then invoke it with:

```text
Use $resume-screening ...
```

或：

Or:

```text
使用 $resume-screening ...
```

## 隐私 / Privacy

不要将真实简历、候选人报告、招聘需求、面试记录或其他招聘隐私材料提交到这个 public 仓库。仓库中的 `.gitignore` 已经屏蔽了常见的本地筛选输入和输出文件，但提交前仍应人工检查文件列表。

Do not commit real resumes, candidate reports, job requisitions, interview notes, or other private recruiting materials to this public repository. The included `.gitignore` blocks common local screening inputs and outputs, but you should still review files before committing.

## 说明 / Notes

这个 Skill 是招聘决策辅助工具，不是自动化录用或淘汰系统。正式招聘决策前仍需要人工复核。

This skill is decision support, not an automated hiring decision system. Human review is required before making recruiting decisions.
