# Resume Screening Skill

A reusable AI skill for screening candidate resumes against hiring requirements. It helps Claude, Codex, or other skill-compatible agents produce structured, evidence-based recruiting recommendations.

## What It Does

- Compares a resume with a job description or hiring requirement.
- Separates must-have requirements, nice-to-have requirements, and disqualifiers.
- Scores candidates with a reusable 100-point rubric.
- Flags missing evidence and interview risks.
- Generates practical interview questions.
- Supports both single-candidate screening and batch candidate ranking.
- Keeps evaluation focused on job-related criteria.

## Repository Structure

```text
.
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
|-- references/
|   `-- screening-rubric.md
`-- .gitignore
```

## Usage

Use the skill with a hiring requirement and one or more resumes:

```text
Use $resume-screening to evaluate this candidate resume against the hiring requirement and recommend whether to proceed to interview.

Hiring requirement:
...

Resume:
...
```

For Chinese hiring workflows:

```text
使用 $resume-screening，根据下面的招聘需求和候选人简历，判断是否建议进入面试。

招聘需求：
...

简历：
...
```

## Output

The skill produces a structured screening report with:

- interview recommendation
- fit score
- confidence level
- candidate profile
- requirements match table
- risk table
- score breakdown
- interview questions
- next-step recommendation

For multiple candidates, it also provides a ranking table and candidate-pool summary.

## Install

### Claude

Copy this folder into your Claude skills directory, or import it through your Claude-compatible skills workflow:

```text
resume-screening/
|-- SKILL.md
|-- agents/openai.yaml
`-- references/screening-rubric.md
```

### Codex

Copy the skill folder into your Codex skills directory, for example:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills\resume-screening"
Copy-Item -Force "SKILL.md" "$env:USERPROFILE\.codex\skills\resume-screening\SKILL.md"
Copy-Item -Recurse -Force "agents" "$env:USERPROFILE\.codex\skills\resume-screening\agents"
Copy-Item -Recurse -Force "references" "$env:USERPROFILE\.codex\skills\resume-screening\references"
```

Then invoke it with:

```text
Use $resume-screening ...
```

## Privacy

Do not commit real resumes, candidate reports, job requisitions, interview notes, or other private recruiting materials to this public repository. The included `.gitignore` blocks common local screening inputs and outputs, but you should still review files before committing.

## Notes

This skill is decision support, not an automated hiring decision system. Human review is required before making recruiting decisions.
