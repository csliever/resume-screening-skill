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

## 支持格式 / Supported Formats

### 招聘需求 / Hiring Requirements

推荐格式：

- 直接粘贴的文本
- `.txt`
- `.md`

可兼容格式：

- `.docx`、`.pdf`、网页 JD、招聘平台导出的内容，只要当前 AI 工具或工作流能够读取并提取其中的文本
- 表格中的岗位要求，例如 `.xlsx`、`.csv`，但建议先整理为文本化的岗位职责、必备条件、加分项和淘汰条件

Recommended formats:

- pasted plain text
- `.txt`
- `.md`

Compatible formats:

- `.docx`, `.pdf`, web job descriptions, or exported recruiting-platform content, as long as your AI tool or workflow can read and extract the text
- spreadsheet-based requirements such as `.xlsx` or `.csv`, preferably converted into clear responsibilities, must-have requirements, nice-to-have requirements, and disqualifiers

### 候选人简历 / Candidate Resumes

推荐格式：

- 直接粘贴的简历文本
- `.txt`
- `.md`

可兼容格式：

- `.docx`
- 可复制文本的 `.pdf`
- 招聘平台导出的简历文本
- 多候选人批量筛选时，可以使用按候选人分段的 `.txt` 或 `.md`

限制：

- 扫描版 PDF、图片简历、截图简历需要先 OCR 成可读取文本。
- 简历排版、图表、头像、证书截图等视觉信息不会作为主要判断依据。
- 如果文件内容无法被当前 AI 工具读取，请先复制出文本再使用。

Recommended formats:

- pasted resume text
- `.txt`
- `.md`

Compatible formats:

- `.docx`
- text-selectable `.pdf`
- resume text exported from recruiting platforms
- for batch screening, `.txt` or `.md` files split clearly by candidate

Limitations:

- scanned PDFs, image resumes, and screenshots should be OCR-processed into readable text first
- visual layout, charts, profile photos, and certificate screenshots should not be treated as primary screening evidence
- if your AI tool cannot read the file directly, extract or paste the text before using the skill

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
