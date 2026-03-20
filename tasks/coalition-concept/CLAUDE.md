# Coalition Concept — CLAUDE.md

## Goal
Produce a polished Quarto brief (PDF + HTML) that defines a compelling Fediverse coalition identity for funders and partners.

The Quarto document is built from the [`quarto-thesis` template](https://github.com/nmfs-opensci/quarto-thesis.git).

---

## Subtasks

Work through these in order. Each produces a concrete file or section.

### 1. Scaffold the Quarto project
- Clone the template into this folder:
  ```
  git clone https://github.com/nmfs-opensci/quarto-thesis.git .
  ```
- Rename `_quarto.yml` fields: title, author, date.
- Set `format: pdf` as the primary output in `_quarto.yml`.
- Commit as `feat: scaffold quarto-thesis template`.

### 2. Brand pillars chapter (`01-brand.qmd`)
Write a chapter covering:
- 3–5 candidate coalition names with a one-line rationale each (e.g. "Public Social Alliance", "Digital Commons Network", "Open Fediverse Fund").
- Brand pillars: openness, sovereignty, sustainability, trust.
- Messaging matrix: audience → key message → proof point.

### 3. Partner shortlist chapter (`02-partners.qmd`)
Create a table of anchor partners:

| Organisation | Type | Why relevant | Contact status |
|---|---|---|---|
| FediVariety | Infrastructure | ... | ... |
| Waag | Public interest tech | ... | ... |
| ProcoliX | Hosting co-op | ... | ... |
| Municipalities (TBD) | Public sector | ... | ... |
| Public broadcasters (TBD) | Media | ... | ... |
| Academic labs (TBD) | Research | ... | ... |

### 4. Pitch deck outline chapter (`03-pitch.qmd`)
Sections:
1. Problem statement — fragmentation, platform risk, digital sovereignty gap
2. Solution — federated public infrastructure
3. Coalition model — governance, membership tiers, decision-making
4. Funding ask — total amount, tranches, milestones
5. Impact metrics — reach, sustainability indicators, public value proxies

### 5. Funding landscape scan (`04-funding.qmd`)
Table of relevant programmes:

| Programme | Funder | Buzzwords to use | Deadline cycle | Fit score |
|---|---|---|---|---|
| NGI Zero | NLnet | trustworthy internet, open standards | rolling | high |
| Digital Democracy Fund | ... | ... | ... | ... |
| Public Interest Tech | ... | ... | ... | ... |

Include a 2–3 paragraph narrative on framing Fediverse infrastructure as essential public digital goods.

### 6. Outreach plan (`05-outreach.qmd`)
- Email/letter templates for each funder tier (foundations, public sector, corporate sponsors).
- Timeline table: Month 1–6 with milestones.
- Decision tree: which funders to approach in parallel vs. sequentially.

### 7. Artefacts checklist appendix (`appendix-checklist.qmd`)
Checkbox list of everything needed for a full proposal:
- [ ] Pitch deck (slides)
- [ ] 2-page executive summary
- [ ] Budget template
- [ ] Partner letters of intent
- [ ] Impact measurement framework
- [ ] Legal entity confirmation

### 8. Bibliography & references (`references.bib`)
Add citations for any statistics, frameworks, or reports referenced in chapters 1–6.

### 9. Render & QA
- Run `quarto render --to pdf` locally and fix any LaTeX errors.
- Check that all cross-references resolve.
- Confirm the PDF is ≤ 30 pages.

### 10. Tag a release
- Commit all changes.
- Push and create a version tag (`git tag v0.1 && git push origin v0.1`).
- The GitHub Actions workflow will automatically build the PDF and attach it to a GitHub Release.

---

## GitHub Actions workflow

The workflow lives at `.github/workflows/build-pdf.yml` (repo root).

**What it does:**

| Trigger | Result |
|---|---|
| Push a `v*` tag (e.g. `v0.1`) | Builds PDF → creates a GitHub Release with the PDF attached |
| Push a `.qmd` / `.yml` / `.bib` file in this folder | Builds PDF → uploads as a workflow artifact (30-day retention) |
| Manual trigger (Actions tab → "Run workflow") | Same as push — useful for testing |

**How to use it:**

1. Make sure the repository is on GitHub and Actions are enabled.
2. The workflow uses `GITHUB_TOKEN` (auto-provided) — no extra secrets needed.
3. To publish a versioned PDF:
   ```bash
   git tag v0.1 -m "First coalition concept draft"
   git push origin v0.1
   ```
   The PDF will appear under **Releases** on GitHub within a few minutes.
4. To download a draft PDF without making a release:
   - Go to **Actions → Build Quarto PDF → latest run → Artifacts**.
5. If the render fails, check the Actions log for LaTeX errors. Common fixes:
   - Missing package: add `tlmgr install <package>` to the workflow's TinyTeX step.
   - R package missing: add it to `renv.lock` or the workflow's R setup step.

---

## File layout (target state)

```
tasks/coalition-concept/
├── CLAUDE.md               ← this file
├── task.md                 ← original task brief
├── _quarto.yml             ← project config (title, author, format)
├── index.qmd               ← front matter / executive summary
├── 01-brand.qmd
├── 02-partners.qmd
├── 03-pitch.qmd
├── 04-funding.qmd
├── 05-outreach.qmd
├── appendix-checklist.qmd
├── references.bib
└── _output/                ← rendered PDF lives here (git-ignored)
```
