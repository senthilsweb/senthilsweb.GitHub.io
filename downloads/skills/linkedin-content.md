---
name: linkedin-content
owner: Senthilnathan
github: https://github.com/senthilsweb
description: Write LinkedIn posts, promo posts, long-form articles, or carousel/cheatsheet one-pager PDFs in Senthil's plain-English practitioner voice. Use this skill whenever Senthil asks for a LinkedIn post, article, promo, caption, cheatsheet, carousel, or any content he intends to publish — even if he just says "draft something about X" or pastes content to redraft — because his voice rules and carousel PDF pipeline must always be applied.
---

# LinkedIn Content in Senthil's Voice

## Defaults vs rules

The **voice rules** below are hard rules — they came from repeated corrections and hold
for every piece. Everything else in this file (sizes, step counts, variant counts,
palettes, layout) is a **default**: a sensible starting point for the common case, not a
constraint on the content. When source material does not fit a default, follow the
material and say what was changed and why. Never compress, pad, or reshape real content
just to satisfy a number written here. If a default turns out to be wrong for a whole
class of work, fix this file rather than working around it each time.

## Voice rules (apply to everything; each was a repeated correction)

1. Simple Indian-style English — his natural voice. Plain words, short sentences.
2. No fancy jargon ("boxes and connections", not "zones and flow"; "read from the prompt", not "parsed").
3. Grounded — no hallucination, no twisting facts into achievements. Honest trade-offs stated, not hidden.
4. No superlatives, no hype, no emojis, no boasting or effort-flexing.
5. Narrative arc for stories: how it used to be done → the gap → what solves it now. Lead with the human habit, not the technology.
6. Articles: neutral third-person voice (no I/my/you). Promo posts: authentic first person.
7. Hashtag `#AdaptiveDataGovOps` for data governance topics; otherwise 4-5 relevant tags at the end.
8. Mask any secrets/API keys that appear in source material (e.g. `nvapi-xxxx...`) and tell him to rotate the real one.
9. Structured comparisons as tables, not ASCII diagrams; image placeholders where a diagram belongs.

## Deliverables by type

- **Post / promo**: 2 variants with different hooks (e.g. name-up-front vs story-first). Short caption options (2-3 lines) on request. A standalone post (no article) gets its own slugified folder under `linkedin-posts/<post-slug>/` in the task-register repo — `post.md` holding the variants, plus that post's cover images and any build script, all inside that folder. **Posts and articles are kept apart on purpose**: `linkedin-posts/` for post-only pieces, `article-drafts/` for articles. Never put a post-only piece in `article-drafts/`, and never put a post's covers at the repo root. Post files need no YAML frontmatter — that requirement is for articles only. Keep each variant under LinkedIn's 3000-character limit and state the character count on delivery. Mermaid/ASCII diagrams do not render in a LinkedIn post — put the diagram in the cover image instead.
- **Article**: Medium-style markdown for LinkedIn's article editor, full URLs so they auto-link, saved as a `.md` file. **Every article file MUST begin with the YAML frontmatter block from the `article-writing` skill** — title, slug, description, date, published: false, type, category, author, sort_order, tags, in that exact order (schema lives in `skills/article-writing/SKILL.md`; this was missed once, do not skip it). All file and folder names slugified (lowercase, hyphens). Each article gets its own slugified folder under `article-drafts/` in the task-register repo, with its cover images inside that folder — never at the repo root.
- **Carousel / cheatsheet PDF**: see pipeline below. Always offer 4-5 title options with a recommendation, plus 2-3 line caption options.

## Carousel/cheatsheet PDF pipeline

**These are defaults, not fixed rules.** Every number below is a starting point that
the content or Senthil's request can override. Do not force source material to fit a
default — if a default fights the content, follow the content and say what was changed.

1. **Canvas.** Default `@page { size: 800px 1000px; margin: 0 }`. Use another size when
   asked or when the destination needs it — 1080×1350 for a carousel page, 1279×720 for
   a cover, A4 landscape for a printable handout. Minimalist layout, generous whitespace.
2. **Color.** Prefer a palette from the `linkedin-cover-generator` palette system over
   inventing colors — that keeps every asset in one visual family. A dark theme is the
   usual default for a single sheet, but light palettes are equally valid, and Senthil
   may ask for the sheet in *every* palette. When the topic has a real brand color, use
   it (NVIDIA green `#76B900`, Copilot blue `#58a6ff`; his own brand teal `#0D7377`).
   Type: Space Grotesk / Inter / JetBrains Mono when available, otherwise a clean system
   sans. Check contrast on pale palettes — a pale accent on a cream background is
   unreadable; drop to the palette's `secondary` for text on light backgrounds.
3. **Step count follows the content — never force a number.** A how-to or setup guide is
   usually 3-5 steps. A reference sheet, lifecycle, or checklist may legitimately be
   10-12, and compressing it would destroy the point of the sheet. Group items into
   phases only when grouping genuinely helps scanning, and ask first if grouping would
   drop detail. Whatever the count, it must fit one page at a readable size — shrink
   spacing before shrinking type, and if it still does not fit, offer a second page
   rather than cutting content silently.
4. **Render** HTML → PNG/PDF with Playwright/Chromium; if the browser download is
   blocked, fall back to WeasyPrint (Liberation Sans) and say so. Render PNGs at
   `device_scale_factor=2` and downsample to the target size for sharp type. When both
   PNG and PDF are requested, generate both from the same page in the same run so they
   cannot drift, and use `print_background=True` for the PDF.
5. **Inspect before delivering.** Preview the PNG and put at least one PDF back through
   `pdftoppm` — backgrounds and accent fills are what break in print, and a PDF that
   lost its background is not obvious from the PNG. For a multi-palette set, build a
   contact sheet and check the whole set in one look.
6. One footer line; no safety-tip filler unless asked. Clean up intermediate `.html`
   files so only the deliverables remain in the folder.
7. **File naming** follows `linkedin-cover-generator`: `<slugged-title>-<palette>-<effect>.<ext>`,
   with the slug and effect held in named constants at the top of the build script.

## Series context

He runs multi-part technical series (e.g. the 6-part Job Match Agent series covering AI-DLC: 11 Bolts, 62 tasks, 135 evals). When drafting a series part, reference the ledger numbers exactly and tease the next part briefly. Note: "AI-DLC" also exists as an AWS term — if confusion is possible, add a one-line clarifier and his repo link.

## Examples

### Example 1 — promo post

User: "Draft a LinkedIn post about part 3 of the Job Match Agent series."

The skill writes 2 variants with different hooks (name-up-front vs story-first), first person, plain English, exact ledger numbers from the series (11 Bolts, 62 tasks, 135 evals), a brief tease of the next part, and 4-5 hashtags.

### Example 2 — article

User: "Turn these notes into a LinkedIn article about the privacy shield project."

The skill writes a Medium-style markdown article in neutral third-person voice, full URLs so they auto-link, saved under its own slugified folder in `article-drafts/` with any cover images inside that folder.

### Example 3 — cheatsheet PDF

User: "Make a one-page cheatsheet on the NVIDIA API setup."

The skill builds the dark-theme 800×1000 HTML page with NVIDIA green accents, renders it to PDF with Playwright (WeasyPrint fallback, stated if used), inspects it with pdftoppm, masks the API key in any screenshot content and tells him to rotate it, and offers 4-5 title options plus 2-3 line captions.

### Example 4 — post plus covers in every palette

User: "Create a subtle post (just post, no article) with cover images in all palette combinations."

The skill writes 2 post variants into `linkedin-posts/<post-slug>/post.md` (no frontmatter, character count stated, no mermaid diagram), then hands the cover work to `linkedin-cover-generator`, which renders one 1279x720 image per palette named `<slugged-title>-<palette>-<effect>.png` into that same folder, alongside the build script.

### Example 5 — reference sheet that does not fit the defaults

User: "Short post and a one-page cheatsheet from this content, numbered steps, GitHub link at the bottom, in every palette as PNG and PDF."

The source has 11 lifecycle stages, not the 3-5 the pipeline defaults to. The skill does not compress them: it confirms the choice with Senthil, then builds all 11 numbered steps on one page, renders 8 palettes × PNG + PDF from the same page, checks a PDF back through `pdftoppm`, and writes the short post variants plus title and caption options into `linkedin-posts/<post-slug>/post.md`. Anything the source frames as interview preparation is dropped when he asks for that.
