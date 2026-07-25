---
name: article-writing
owner: Senthilnathan
github: https://github.com/senthilsweb
description: Write or edit blog articles, documentation pages, and LinkedIn promo posts in the author's house style, modeled on the templrgo project's content/blog and content/docs corpus — YAML frontmatter, plain storytelling in layman English, concrete numbers over adjectives, tables for enumerable facts, one true story woven into the narrative (never a labelled "honest aside" or "What's next" section), runnable CTAs, and a short hook-first promo post per article. Use whenever the user asks to draft, revise, or review an article, blog post, docs page, or LinkedIn post/series in this repo (articles-draft/) or any repo following this style.
user-invocable: true
---

# article-writing — my standard blog / docs / promo style

Modeled on and copied from the templrgo project's `content/blog` and
`content/docs` corpus (e.g. `introducing-knowledge-graph.md`,
`about-cv-guide.md`). One markdown file per piece. Promo posts are
separate files so they paste into LinkedIn unedited.

## Blog article frontmatter (required, this order)

```yaml
---
title: "Readable Title — Subtitle If It Earns One"
slug: kebab-case-stable-forever
description: One sentence, ~25 words, states the concrete payload — used for OG/meta, no clickbait
date: 2026-07-12T00:00:00Z
published: false        # flipped to true only when actually published
type: blog
category: Announcements | Engineering | Methodology | Series
author: Senthilnathan (senthilsweb)
sort_order: 10          # series position × 10
tags: [lowercase, kebab-case, 5-to-9-of-them]
---
```

## Docs page frontmatter (the smaller schema)

```yaml
---
title: "Feature Guide"
description: "Complete reference for X — what it covers, in one sentence."
weight: 6               # ordering within the docs section
---
```

Docs live in numbered section folders (`01-overview/`, `03-user-guide/`,
`04-developer/`); user guide and developer guide are separate pages,
never merged.

## Article structure (in order)

1. `# H1` restating the title.
2. **Cold open** — 2–3 sentences delivering the payload immediately
   ("We are shipping…", "The LLM never scores."). No throat-clearing,
   no "In today's fast-paced world".
3. **A "Why?" section early** — the problem in plain English, with the
   question the reader is actually asking in italics.
4. **Body H2s** — short, concrete ("What's in v1.4", "How it works
   (the 60-second tour)"). Tables for enumerable facts; fenced code
   for anything runnable; numbered lists only for real sequences.
5. **One true story, woven in** — a real bug, wrong first attempt, or
   deliberate limitation, told straight and verified against the source
   repo. Weave it into the narrative under a plain topical heading
   ("Paste a link, see the article") — NEVER a section labelled
   "honest aside", "One honest aside", or similar meta-labels. The
   credibility comes from the story, not the label.
6. **Runnable CTA** — the actual command or link, in a code block.
7. **Sign-off** — one line, em-dash + name.
8. **`## Related reading`** — bold-linked list with a one-clause
   description each. Always last.

No "What's next" section by default — if what is not built matters,
say it in one line inside the relevant section. (Senthil, 2026-07-19:
"No need to say 'honest', what's next etc.")

## Voice rules

- **Tell it as a story, in layman English.** Background first ("In 2021
  I built…"), then what it does, in flowing prose a non-engineer can
  follow. Explain the mechanism in plain words ("the preview is built
  by a bot that does not run JavaScript") instead of naming the
  technology and moving on. Prefer narrative flow over labelled
  meta-sections.
- **Simple Indian English, always.** Short direct sentences, everyday
  words. No fancy words ("culmination", "storytelling vehicle",
  "materialized", "structurally", "permanently settled") — prefer the
  plain verb ("built", "ended", "became"). No jargon: if a technical
  term is unavoidable, explain it in the same line in plain words
  ("a Bolt is the sprint, but hours or days, not weeks").
- Concrete numbers over adjectives: "135 evals", "9.58 seconds",
  "≤50 KB" — never "extensive", "blazing fast", "lightweight".
- Short declarative sentences for the big claims. One idea per
  paragraph; 1–3 sentence paragraphs.
- Bold the load-bearing noun on first appearance, not for emphasis.
- First person plural for team work, first person singular only when
  it is genuinely one person's experience or decision.
- Every claim traceable to the source repo/deck; a plan is written as
  a plan ("Phase 2 will…"), never as a shipped fact.
- When the article claims a mechanism — a rubric, a test, a metric, a
  bug — quote the real artifact: a short excerpt of the actual file or
  the actual test name beats a description of it. Verify against the
  source repo before writing; never retell a bug or a fix from memory.
- When evals are discussed, say the type explicitly — deterministic
  (exact assertions) or LLM-as-judge (a second model grades) — and say
  which one the project actually uses.

## Screenshot and visual placeholders

The owner adds many screenshots before publish. Mark every spot where
a visual belongs with an italic placeholder line on its own:

```
*[Screenshot: Arize AX trace waterfall — one 9.58 s run]*
*[Screenshot: pytest output — 109/109 passing]*
```

- Place one wherever the text mentions a UI, a terminal run, a trace,
  a dashboard, or a diagram — web or code alike.
- Observability screenshots (Arize traces, lineage graphs, dashboard
  pages) are always worth a placeholder when the article mentions runs.
- Quoted code and rubric excerpts go in as real fenced blocks
  immediately; only images get placeholders.
- No emoji in articles. No rhetorical questions except the italicized
  reader-question in the Why section.

## LinkedIn promo post (one per article, separate `-promo.md` file)

- ≤180 words, no markdown headings — LinkedIn renders plain text.
- Line 1 is the hook and must survive alone: it is all the feed shows
  before "…see more". A number or a contrarian claim beats a topic
  statement.
- Short line-broken paragraphs (1–2 sentences each), one blank line
  between them.
- One `[LINK]` placeholder for the article URL, near the end.
- 3–5 hashtags on the final line, camelCase multiword
  (`#PydanticAI #AIEngineering`).
- No fabricated engagement bait ("Agree?"), no "I'm humbled/excited to
  announce". The article's best fact is the post.

## Series conventions

- Every part opens with `Part n of 6` (or series length) and a linked
  list of all parts; unpublished parts use `[LINK-PART-n]`
  placeholders, replaced as each publishes.
- Shared CTA block verbatim in every part, so any entry point promotes
  the same repos/demo.
- The final part doubles as the recap and full index of the series.

## Examples

### Example 1 — new blog article

User: "Draft the release article for v1.4 of the project."

The skill writes one markdown file with the full frontmatter block, a cold open that delivers the payload in 2-3 sentences, an early story-style "why" section, concrete-numbered body H2s with tables for enumerable facts, one true story (a real bug or wrong turn, verified against the source repo) woven in under a plain topical heading, a runnable CTA, the em-dash sign-off, and `## Related reading` last — plus screenshot placeholders wherever a UI or terminal run is mentioned.

### Example 2 — promo post for an existing article

User: "Write the LinkedIn promo for the knowledge-graph article."

A separate `-promo.md` file: ≤180 words, no headings, a first line that survives alone in the feed, short line-broken paragraphs, one `[LINK]` placeholder near the end, 3-5 camelCase hashtags on the final line. The article's best fact is the post.

### Example 3 — series part

User: "Draft part 4 of the series."

Opens with `Part 4 of 6` and the linked list of all parts (`[LINK-PART-n]` placeholders for unpublished ones), reuses the shared CTA block verbatim, and follows the same article structure as Example 1.
