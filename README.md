# skill-resume-tailor

A Claude skill that tailors Yaswanth's resume to a specific job description and outputs polished, compilable LaTeX.

## Trigger
Say: `tailor my resume for this JD`, `tailor resume`, or paste a JD and ask for a resume.

## What it does
- Reads the bundled base resume (`references/base-resume.tex`)
- Rewrites summary, experience bullets, projects, and skills to match the JD
- Outputs complete LaTeX — no fragments
- Optionally generates a cover letter
- `updateBaseResume` keyword triggers a guided base update flow

## Files
- `SKILL.md` — skill instructions
- `references/base-resume.tex` — base resume source
