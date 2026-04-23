# Resume Project Rules

Rules for working on `Sahas_Goli_Resume.tex` (and the rendered PDF).

## Source of truth

- `Sahas_Goli_Resume.tex` is the authoritative resume. Edit the `.tex`, rebuild, and commit both `.tex` and `.pdf`.
- There is no `.md` counterpart anymore — do not recreate one.
- The repo is served as GitHub Pages from `sahas266.github.io`. `index.html` embeds the PDF and should not be modified casually.

## Build and verify workflow

After any content edit, always:

1. Rebuild: `pdflatex -interaction=nonstopmode Sahas_Goli_Resume.tex`
2. Re-extract to check line wraps: `pdftotext Sahas_Goli_Resume.pdf -`
3. For visual verification, render: `pdftoppm -r 200 -png Sahas_Goli_Resume.pdf preview` then read `preview-1.png`.
4. Confirm the document is still **one page** (`pdfinfo Sahas_Goli_Resume.pdf | grep Pages`).

Never report a change as done before rebuilding and verifying line fit.

## Single-page rule

The resume must fit on one page. If a change pushes it to two, either:

- Revert the change, or
- Ask the user which content to trim before proceeding.

Don't silently reduce fonts or margins to force a fit.

## Bullet-length rules

Every bullet must take as **few lines as possible** and **fill as much of each line as possible**. Concretely:

- If a bullet fits on one line, it must be on one line — do not pad it to feign depth.
- If a bullet must span multiple lines, minimize the line count, and every line except possibly the last should be substantially full (no words hanging on an otherwise empty line).
- A short tail on the final line — e.g., just "graph." or "engine." — means the bullet is slightly too long. Trim the minimum number of words to either (a) pull the tail up onto the previous line, or (b) lengthen the bullet so the last line is substantially filled. Never leave a lone-word tail.

"Lines" are determined by actual PDF wrapping — verify via `pdftotext`, and for borderline cases render `preview-1.png` and inspect visually.

Most bullets should fit on exactly **one line**. Only these two bullets may span **two full lines**:

- Cornell Blockchain: Phantom Pool bullet
- Cornell Blockchain: Rust causal-inference engine bullet

## Editing bullets

When asked to condense an overflowing bullet:

- Preserve information — move content between bullets if needed rather than deleting it.
- Prefer removing redundant qualifiers ("data" before "warehouse", "analysis" after "sentiment analysis") over removing specifics like numbers, technologies, or named entities.
- Keep specific claims (percentages, AUM figures, competition names, project names, named collaborators like White Star Capital) intact.

When asked to add a bullet, check wrap behavior immediately after and condense if it exceeds the allowed lines.

## Content accuracy

Don't invent technical claims. If a bullet references a project or tool, check the underlying source (e.g., the project's repo) before writing specifics. Examples of claims to never fabricate:

- Model types (don't write "NLP sentiment" if the code has no NLP)
- Metrics (don't invent percentages, row counts, or accuracy figures)
- Collaborators (don't add firm names the user didn't mention)

When the user provides an exact bullet, use it verbatim — do not rephrase unless asked.

## LaTeX conventions in this file

- Special chars that need escaping in bullet text: `%` → `\%`, `$` → `\$`, `&` → `\&`, `#` → `\#`, `_` → `\_`.
- Date ranges use `--` (en-dash), not `-`.
- Bolded inline text: `\textbf{...}`. Italic: `\textit{...}`. Currently **no bold is used inside bullet text** — only at the subheading level and the skills/achievements/languages labels.
- Font: Times New Roman via `mathptmx`. Base size 11pt; bullets render at `\small`.
- The custom commands `\resumeSubheading`, `\resumeItem`, `\resumeItemListStart/End` are tuned for current spacing. Do not modify these unless the user explicitly asks for a spacing change.

## Section structure (do not reorder)

1. Header (name + contact line)
2. Education
3. Professional Experience (reverse chronological)
4. Projects & Outside Experience (reverse chronological)
5. Additional Information (Skills, Achievements, Languages — in that order)

## Git workflow

- Commit both `Sahas_Goli_Resume.tex` and `Sahas_Goli_Resume.pdf` together. The PDF is tracked so GitHub Pages can serve it.
- Never commit LaTeX build artifacts (`.aux`, `.log`, `.out`, `.fls`, `.fdb_latexmk`, `.synctex.gz`, `preview-*.png`) — they are gitignored.
- Commit messages: imperative, one-line subject, no body unless the change is non-obvious.

## What to push

Before `git push`:

- Rebuild the PDF so the committed binary matches the `.tex`.
- Confirm 1 page.
- Stage only `Sahas_Goli_Resume.tex`, `Sahas_Goli_Resume.pdf`, and any intentionally-modified repo files (e.g., `index.html`, `.gitignore`, `CLAUDE.md`). Don't `git add -A` without checking.
