---
name: resume-tailor
description: |
  Tailor Yaswanth's resume to a specific job description and output polished LaTeX code.
  Trigger whenever the user says "tailor my resume", "tailor resume", "tailor for this JD",
  or pastes a job description and asks for a resume. Also trigger for "cover letter" requests
  and when the keyword "updateBaseResume" is used. Always use this skill for any resume,
  CV, or cover letter task — even if the request seems simple.
---

# Resume Tailor Skill

Tailor Yaswanth's resume to a given job description and return complete, compilable LaTeX code.

---

## Base Resume

The base resume is stored in this skill's memory (see `references/base-resume.tex`). It contains:
- LaTeX preamble and formatting (do NOT alter the document structure or preamble)
- Fixed personal details: name, GitHub, LinkedIn, email
- Canonical project list and work experience
- Skills table

**Always treat `references/base-resume.tex` as the source of truth.** If the user invokes `updateBaseResume`, ask for the new `.tex` content and update that file.

---

## Tailoring Instructions

### 1. Summary
- Rewrite entirely to mirror the JD's language, priorities, and role framing
- 3–5 sentences, no first-person pronouns ("I"), no fluff
- Lead with the role type from the JD (e.g. "Data Engineer", "ML Engineer", "AI Researcher")
- Weave in JD keywords naturally — this is the ATS hook
- Keep it punchy; avoid AI-ism phrases like "passionate about", "proven track record", "dynamic"

### 2. Work Experience (AI/ML Trainee — Maghil)
- Keep the job title and dates unchanged
- Rewrite bullet points to emphasise skills/tools mentioned in the JD
- Reorder bullets so the most JD-relevant ones appear first
- Add quantified impact where plausible (%, time saved, scale)
- Max 6 bullets; remove irrelevant ones

### 3. Projects
**Decision logic (apply in order):**
1. If an existing project maps well to a JD requirement → **keep and reframe** its description to highlight the relevant angle
2. If an existing project partially maps → **stretch** it — emphasise the parts that relate, add a plausible detail if needed
3. If the JD calls for something with no existing project → **invent a new plausible project** using Yaswanth's known stack (Python, GCP, TensorFlow, PyTorch, Gemini API, BERT, RAG, Pinecone, Cohere, Streamlit, Docker, SHAP, Grad-CAM)

**Invented projects must be:**
- Technically plausible given his background
- Specific enough to be credible (tool names, approach, outcome)
- Not contradicting anything on the base resume

**Ordering:** Always reverse chronological — most recent at the top. Assign a plausible date to new projects (use recent months if unspecified).

**Per-project description:** 2–3 lines max. Lead with what was built, then the tools/approach, then the outcome or metric.

### 4. Skills
- Remove skills irrelevant to the JD
- Reorder categories and items within categories to front-load JD-relevant ones
- Add new skills/tools from the JD **if they are within Yaswanth's plausible reach** (e.g. if JD mentions LangChain and he works with RAG pipelines, add it)
- Do NOT add skills that are clearly outside his background (e.g. iOS development, C++)
- Keep the tabular format intact

### 5. Formatting Rules (never break these)
- Output must be complete, compilable LaTeX — include the full preamble
- Do not change the document class, geometry, or font settings
- Do not change personal contact details
- Do not add new LaTeX sections (Education stays as-is)
- Keep all existing LaTeX environments (`joblong`, `tabularx`, etc.)
- Escape special characters properly: `&`, `%`, `$`, `#`, `_` etc.

---

## Cover Letter

When a cover letter is requested:

1. **Do NOT output LaTeX** — output plain text only
2. Analyse the JD tone (formal, startup-casual, corporate, technical) and mirror it
3. Structure:
   - **Para 1:** Hook — why this role/company, one specific thing from the JD or company
   - **Para 2:** Most relevant experience + 1–2 concrete examples from resume
   - **Para 3:** A project or skill that directly addresses a JD requirement
   - **Para 4:** Short close — enthusiasm, availability, next step
4. After drafting, apply the **humanizer skill** (`/mnt/skills/user/humanizer/SKILL.md`) to remove AI-ism patterns before returning the final version
5. Target length: 250–350 words

---

## updateBaseResume

If the user says `updateBaseResume`:
1. Ask: *"Please paste the new base resume LaTeX content and I'll update it."*
2. Once provided, update `references/base-resume.tex` with the new content
3. Confirm: *"Base resume updated. Future tailoring will use this version."*

---

## Output Format

For resume tailoring:
- Return the **full LaTeX document** in a code block (```latex ... ```)
- Follow with a brief bullet list of the key changes made (summary, which projects added/modified, skills adjustments)
- Do not ask clarifying questions unless the JD is too vague to extract a role type

For cover letters:
- Return the humanized plain-text cover letter
- No preamble, no explanation — just the letter

---

## Quick Reference — Yaswanth's Known Stack

| Domain | Tools |
|---|---|
| Languages | Python, R, Java |
| ML/DL | TensorFlow, PyTorch, scikit-learn |
| NLP/LLMs | BERT, Gemini API (Flash 2.0/2.5/2.5-pro), RAG pipelines, Cohere, LangChain |
| Vector/Search | Pinecone |
| Cloud | GCP |
| Explainability | SHAP, Grad-CAM |
| Data | Pandas, NumPy, Hadoop, Spark |
| Databases | MySQL, PostgreSQL, MongoDB, Cassandra, Neo4j |
| Viz/Analytics | Matplotlib, Tableau, Excel, Orange |
| Dev Tools | Streamlit, Flask, Docker, GitHub, VSCode, Jupyter |
