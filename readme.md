# JOB_APPLIER.md: Claude Resume and Cover Letter Agent

A Claude skill that takes a job description and generates a tailored, ATS-optimized resume and cover letter as downloadable PDFs. Your resume data lives hardcoded in the skill file, so every run is fast, consistent, and requires no re-uploading.

---

## Requirements

- A [Claude.ai](https://claude.ai) account (free tier works)
- **Code execution must be enabled** in your Claude settings. This is what allows Claude to generate the PDFs. If you don't see file downloads after running, check that this feature is turned on under Settings > Feature Preview.

---

## How It Works

Claude reads your hardcoded resume profile, parses the job description you paste in, and outputs two PDFs:

1. A tailored, ATS-safe resume with bullets reworded to mirror the job description's language
2. A cover letter written to match the company's tone and culture

After both PDFs, Claude appends a **Fit Assessment** with an honest read on match strength, potential gaps, and suggested interview talking points.

---

## Setup

### 1. Keep your resume in Google Docs

Maintain a living document in Google Docs as your source of truth. Add every role, project, and bullet you might want. You will trim and reorder per job. When ready to update the skill, go to **File > Download > Markdown (.md)**.

### 2. Open `JOB_APPLIER.md`

Open the file in any text editor. The **Candidate Profile**, **Experience**, and **Recent Projects** sections near the top are where your resume data lives.

### 3. Find and replace all `DG_REPLACE_` tokens

Every piece of personal information is marked with a `DG_REPLACE_` prefix. Do a global find (Ctrl+H / Cmd+H) for `DG_REPLACE_` to surface all tokens at once, then replace each with your own details. The full token reference table is at the top of the skill file.

### 4. Update the resume content sections

After replacing tokens, paste your actual resume content into the **Candidate Profile**, **Experience**, and **Recent Projects** sections. The rules, enforcement logic, and output instructions can stay as-is.

### 5. Delete the setup block

The setup instructions at the top of the file are for your reference only. Delete everything above the line that reads `You are an expert technical resume writer...` before uploading to Claude.

### 6. Create a Claude Project and upload the skill file

Go to [claude.ai](https://claude.ai), create a new Project, and upload your completed `JOB_APPLIER.md` as a Project file. Claude will reference it automatically in every conversation inside that project.

### 7. Paste a job description and run

Start a new conversation inside the project and send:

```
Here is a job description. Generate a tailored resume and cover letter as PDFs.

[paste job description here]
```

Claude will parse the posting, flag any hard requirements you don't meet, tailor your resume, write a cover letter, and generate both as downloadable PDFs.

### 8. Download and review

Download both PDFs. Read them carefully, not just for accuracy, but for anything worth carrying back into your master Google Doc. Good tailored bullets often improve your base resume.

### 9. Make final edits if needed

- **Minor tweaks** (a word, spacing, alignment): open the PDF in **LibreOffice Draw** for quick edits without regenerating.
- **Structural changes** (reordering sections, rewriting bullets, adjusting tone): describe what you want in chat and ask Claude to regenerate.

---

## What the Skill Enforces 

**No fabrication.** Claude will never add skills, tools, or accomplishments not present in your profile. If a job description lists a required skill you don't have, Claude flags it before generating rather than silently including it.

**Skill gap flagging.** If a JD requirement is not in your profile, Claude surfaces it in a pre-generation note so you decide whether to proceed, not Claude.

**Em-dash removal at the code level.** Em-dashes (U+2014) break ATS parsers and are a strong AI-writing signal. The skill asserts the character is absent from both documents before calling PDF generation. If one slips through the writing phase, the build fails and Claude rewrites before proceeding.

**Human-sounding cover letters.** The skill includes explicit anti-AI writing rules: no significance inflation, no filler openers, no uniform sentence length, no rule-of-three synonym cycling. The goal is a letter that reads like you wrote it on a good day.

---

## Files

| File | Description |
| --- | --- |
| `JOB_APPLIER.md` | The skill file. Fill in your resume here before use. All PII replaced with `DG_REPLACE_` tokens, safe to fork. |
| `readme.md` | This file. |

---

## Tips

- **Update your skill file after every application.** When Claude writes a bullet that is better than yours, carry it back into your Google Doc. The skill gets sharper as your profile does.
- **Start a fresh conversation per job.** Claude Projects persist the skill file, but each job should be its own conversation to avoid bleed between tailoring decisions.
- **Be honest in your profile.** The no-fabrication rule only works if your source data is accurate. The skill reframes and reorders; it does not invent.
