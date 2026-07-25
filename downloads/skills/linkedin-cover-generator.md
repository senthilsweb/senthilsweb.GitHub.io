---
name: linkedin-cover-generator
owner: Senthilnathan
github: https://github.com/senthilsweb
description: Generate polished LinkedIn cover images (article covers, promo cards, profile banners, feed images, carousel pages) from an article, post draft, short idea, local file, or remote URL — editorial left-text / right-visual layout, curated palette system, safe-area rules, and an approval-before-generation workflow. Use whenever Senthil asks for a cover image, banner, promo card, or social image for LinkedIn or an article — even if he just says "create a cover for this post".
user-invocable: true
---

# linkedin-cover-generator — LinkedIn cover image generator

## Defaults vs rules

Hard rules in this file: the **file naming** convention, the **where the files go**
convention, the **safe-area** margins, and the **brand and safety** rules. Everything
else — sizes, density, palette choices, the topic-to-visual map, chip counts — is a
default or a lookup, chosen for the common case.

The `topic_visuals` and palette-selection tables below are illustrative, not exhaustive.
A topic that is not listed is normal: pick the closest match or compose a new visual, and
add the new entry to this file if the topic is likely to recur. Never bend the content to
fit a listed topic just because it is listed.

## Purpose

Generate polished LinkedIn cover images from an article, post draft, short idea, local file, or remote URL. The goal is to create a professional article-cover or promo-card image that follows a consistent editorial style while adapting the visual theme, palette, wording density, and layout to the topic.

This skill is intended for technical thought-leadership posts, open-source project announcements, architecture articles, AI/agent engineering posts, data governance posts, privacy/security posts, and career-positioning content.

---

## Default output standard

Unless the user explicitly requests another size, generate the image using:

```text
1279 × 720 px
```

This is the default LinkedIn article/promo cover size used by this workflow.

### Supported size presets

```yaml
size_presets:
  linkedin_article:
    width: 1279
    height: 720
    description: Default LinkedIn article and promo cover image.
  linkedin_profile_cover:
    width: 1584
    height: 396
    description: LinkedIn personal profile background image.
  linkedin_post:
    width: 1200
    height: 627
    description: General LinkedIn feed image.
  linkedin_square:
    width: 1080
    height: 1080
    description: Square social image.
  linkedin_carousel_page:
    width: 1080
    height: 1350
    description: Portrait carousel page.
  wide_banner:
    width: 1920
    height: 1080
    description: Wide presentation-style banner.
```

### Custom size syntax

Accept any of these user inputs:

```text
size=1279x720
canvas=1279x720
dimension="1279 × 720"
width=1279 height=720
```

Normalize all of them to `{ width, height }`.

---

## File naming (strict — this was missed once)

Every generated image file MUST be named:

```text
<slugged-title>-<palette>-<effect>.png
```

- `<slugged-title>` — the post/article title, slugified (lowercase, hyphens only,
  no spaces or underscores). **Never omit it.** A file called `cover-cream-emerald.png`
  is wrong: once it leaves the folder nobody knows which post it belongs to, and two
  posts in the same repo collide.
- `<palette>` — the palette key from the palette system, hyphenated
  (`cream_emerald` → `cream-emerald`, `blue_pink_gloss` → `blue-pink-gloss`).
- `<effect>` — the visual treatment actually applied: `subtle`, `glossy`, `minimal`,
  `balanced`, or `infographic`.

Example:

```text
building-an-agent-is-only-half-the-job-blue-pink-gloss-subtle.png
```

When generating a set across several palettes, keep the slug and effect identical
across the set so the files sort together and only the palette varies.

If a build script produces the images, put the slug and effect in named constants at
the top of the script so a rebuild cannot drift from the delivered filenames.

## Where the files go

- Cover for a **standalone LinkedIn post** → `linkedin-posts/<post-slug>/`
- Cover for an **article** → `article-drafts/<article-slug>/`

Images always live inside the post's or article's own folder — never at the repo root.

## Input sources

The skill must accept content from any of the following.

### 1. Direct text input

The user may paste the post, article, title, rough notes, or full Markdown body directly in the prompt.

### 2. Local file path

The user may provide a local file path such as:

```text
input=./articles/my-post.md
input=/mnt/data/article.md
input=./drafts/post.txt
```

Supported file types:

```yaml
supported_input_files:
  - .md
  - .markdown
  - .txt
  - .html
  - .htm
  - .json
```

Optional extended support if available:

```yaml
optional_input_files:
  - .pdf
  - .docx
```

For `.pdf` and `.docx`, extract readable text first. Do not rely on visual screenshots unless the task specifically requires visual interpretation.

### 3. Remote URL

The user may provide:

```text
input=https://example.com/article
input=https://raw.githubusercontent.com/user/repo/main/article.md
input=https://github.com/user/repo/path/to/file.md
```

Behavior:

1. Fetch the URL.
2. Detect whether it is raw Markdown, HTML, or plain text.
3. Extract title, subtitle, description, headings, links, and relevant body text.
4. Ignore unrelated navigation, cookie banners, ads, and page chrome.
5. Preserve source links only if the user asks to include them on the image.

### 4. Reference image

The user may provide a visual reference and ask to follow its layout, size, or style.

Behavior:

- Reuse the style direction, not exact copyrighted design elements.
- Preserve the user’s established layout patterns if they refer to earlier successful covers.
- If a reference image is used only for size, match the aspect ratio and composition safety rules.

---

## Content extraction

Extract a concise creative brief from the input.

### Required extraction fields

```json
{
  "title": "",
  "subtitle": "",
  "short_support_line": "",
  "topic": "",
  "category": "",
  "audience": "",
  "core_message": "",
  "keywords": [],
  "must_include_text": [],
  "must_avoid_text": [],
  "links_to_include": [],
  "brand_or_company_names": [],
  "personal_links": [],
  "tone": "",
  "visual_metaphor": "",
  "sensitivity": "normal"
}
```

### Extraction rules

1. Prefer the article title when it is strong and concise.
2. If the title is too long, create a shorter cover title.
3. Keep subtitles short and readable at LinkedIn preview size.
4. Avoid turning the cover into a full summary.
5. Extract only the strongest 3–5 concepts for visual chips.
6. Preserve user-specified title text unless it is too long or visually unsuitable.
7. Ask for approval before using employer names, product names, or customer names unless the user explicitly requests them.
8. If the user says “safe play,” “personal post,” “my view,” or “thought leadership,” avoid company/product names and use generic conceptual wording.
9. If the user asks for GitHub, LinkedIn, demo, or repo links, include them as small footer text only.

---

## Default layout pattern

Use the established LinkedIn cover style:

```yaml
layout:
  structure: editorial_left_visual_right
  left:
    - category badge
    - large title
    - short subtitle
    - optional quote or support line
    - 3 to 5 feature chips
  right:
    - abstract visual metaphor OR clean architecture illustration
    - minimal text
    - icons/cards only when useful
  footer:
    - optional small link strip
```

### Safe-area rules

For `1279 × 720`:

```yaml
safe_area:
  margin_left: 56
  margin_right: 56
  margin_top: 48
  margin_bottom: 52
  footer_height_max: 72
```

Rules:

1. Keep main title away from all edges.
2. Do not place important text at extreme bottom.
3. Avoid very small text.
4. If a footer is required, keep it inside a clean footer strip.
5. Do not put important content near corners.
6. Avoid overcrowded right-side diagrams.
7. Prefer fewer words over more words.

---

## Visual density levels

Accept:

```yaml
density:
  minimal:
    description: Executive, abstract, thought-leadership style. Least text.
  balanced:
    description: Title + subtitle + few chips + visual metaphor. Default.
  infographic:
    description: More labeled cards and architecture elements. Use only when requested.
```

Default:

```text
balanced
```

Use `minimal` for personal opinion, thought leadership, career, leadership, or conceptual articles.

Use `infographic` for architecture, workflow, agent pipeline, product walkthrough, or implementation-heavy articles.

---

## Color palette system

Choose a palette based on the article theme and recent visual history. Avoid repeating the same palette in consecutive images unless the user asks for consistency.

### Palette options

```yaml
palettes:
  cream_emerald:
    mood: calm, premium, modern, trustworthy
    best_for:
      - data workflows
      - job-scout agents
      - multi-agent architecture
      - homelab / hands-on engineering
    colors:
      background: "#F8F2E6"
      primary: "#062E2B"
      secondary: "#0B6B55"
      accent: "#D8C98A"
      soft_accent: "#BFD8C8"

  deep_navy_cyan_violet:
    mood: technical, futuristic, engineering-heavy
    best_for:
      - AI agents
      - architecture
      - testing
      - observability
      - distributed systems
    colors:
      background: "#061326"
      primary: "#F8FAFC"
      secondary: "#38DDF5"
      accent: "#8B5CF6"
      soft_accent: "#1E40AF"

  blue_pink_gloss:
    mood: modern, energetic, polished
    best_for:
      - AI era
      - elegant engineering
      - career positioning
      - forward-deployed engineering
    colors:
      background: "#F8F5EE"
      primary: "#071C3A"
      secondary: "#2563EB"
      accent: "#EC4899"
      soft_accent: "#C7D2FE"

  dark_neon_pink_blue:
    mood: bold, futuristic, high-impact
    best_for:
      - AI engineering
      - agent systems
      - technical essays
      - modern software roles
    colors:
      background: "#050B1E"
      primary: "#FFFFFF"
      secondary: "#38BDF8"
      accent: "#F472B6"
      soft_accent: "#7C3AED"

  privacy_orange_coral:
    mood: alert but polished, sensitive data, privacy
    best_for:
      - privacy
      - DLP
      - PII
      - data protection
      - security workflows
    colors:
      background: "#FFF7ED"
      primary: "#111827"
      secondary: "#F97316"
      accent: "#EF4444"
      soft_accent: "#FDBA74"

  light_blue_purple:
    mood: clean, intelligent, data/AI
    best_for:
      - document fingerprinting
      - MinHash
      - LSH
      - data intelligence
      - search/indexing
    colors:
      background: "#EAF6FF"
      primary: "#071C3A"
      secondary: "#2563EB"
      accent: "#7C3AED"
      soft_accent: "#67E8F9"

  charcoal_gold_teal:
    mood: premium, serious, production-grade
    best_for:
      - production systems
      - durable agents
      - frameworks
      - orchestration
    colors:
      background: "#07110F"
      primary: "#F8FAFC"
      secondary: "#14B8A6"
      accent: "#FBBF24"
      soft_accent: "#2DD4BF"

  soft_slate_copper:
    mood: elegant, mature, editorial
    best_for:
      - leadership
      - engineering craft
      - career reflection
      - executive writing
    colors:
      background: "#F6F1EA"
      primary: "#1E293B"
      secondary: "#475569"
      accent: "#B77945"
      soft_accent: "#CBD5E1"
```

### Color selection rules

1. For privacy/DLP/security: prefer `privacy_orange_coral`.
2. For data governance/adaptive operating model: prefer `deep_navy_cyan_violet` or minimalist abstract variant.
3. For job-search/data pipeline agents: prefer `cream_emerald`.
4. For AI engineering / elegant engineering: prefer `blue_pink_gloss` or `dark_neon_pink_blue`.
5. For document fingerprinting / MinHash / LSH: prefer `light_blue_purple`.
6. For multi-agent orchestration/frameworks: prefer `cream_emerald`, `charcoal_gold_teal`, or `deep_navy_cyan_violet`.
7. For homelab and hands-on engineering: prefer soft cream, teal, coral, and light data-catalog style.
8. If user asks “different color than previous two,” avoid the last two used palettes.
9. If user asks “subtle,” reduce saturation and use a soft background.
10. If user asks “glossy,” use glass cards, soft shadows, glow, and polished highlights.

---

## Text generation rules

### Title

The title must be short, high-impact, readable at thumbnail size, no more than 2–3 lines, and ideally under 55 characters.

If the article title is long, create a shorter cover title and preserve the article title in the post, not the image.

### Subtitle

The subtitle should explain the value in one line or two short lines.

Examples:

```text
A Testing Architecture for AI-Augmented Quality Engineering
Near-Duplicate Detection Without AI Embeddings
Orchestrator + Sub-Agents Pattern
Data governance needs an adaptive operating model
How My Homelab Keeps Me Hands-On
```

### Support line

Optional. Use sparingly.

Examples:

```text
AI did not invent elegant engineering. It made it essential.
Build the intelligence once. Make every surface a thin adapter.
Structured. Scalable. Observable.
Data model first • Verify sources • Never fabricate
```

### Chips

Use 3–5 short chips.

Examples:

```text
DuckDB
Deterministic
Referral-First
Agentic Toggle
```

```text
PFC Tree
Pairwise
Observability
Triage
Lint Gates
```

```text
CLI
REST API
Python
MCP Chat
```

```text
Business-first
Testing
Reliability
Security
Reuse
```

---

## Footer link rules

Only include footer links if the user explicitly asks.

Supported footer types:

```yaml
footer_links:
  github:
    icon: GitHub mark or simple code/repo icon
    text_format: "github.com/<user>/<repo>"
  linkedin:
    icon: LinkedIn or profile icon
    text_format: "linkedin.com/in/<handle>"
  live_demo:
    icon: globe or launch icon
    text_format: "<domain>"
  docs:
    icon: document icon
    text_format: "<domain/path>"
```

Rules:

1. Keep footer link text small but readable.
2. Prefer one clean footer strip.
3. If both LinkedIn and GitHub are requested, place LinkedIn on the left and GitHub on the right.
4. Avoid raw `https://` unless the user explicitly wants the full visible URL.
5. For LinkedIn posts, use non-shortened visible links only if the user requests them.
6. Do not invent links.

---

## Brand and safety rules

1. Do not add employer names unless explicitly requested.
2. Do not add product names unless explicitly requested.
3. If a user says “safe play,” avoid company/product/customer names.
4. Do not use official logos unless the user provides them or explicitly requests them.
5. Generic icons are preferred over brand marks.
6. Do not claim certifications, employment status, partnerships, or endorsements.
7. Avoid making the cover look like an official company advertisement unless requested.
8. For personal thought leadership, use “My View” style only if the user asks.

---

## Topic-to-visual mapping

```yaml
topic_visuals:
  ai_augmented_quality_engineering:
    visual:
      - capability folder
      - PFC tree
      - AI agent cards
      - CI lint gate
    chips:
      - PFC Tree
      - Pairwise
      - Observability
      - Triage
      - Lint Gates

  diagram_agents:
    visual:
      - central orchestrator
      - renderer variations
      - reporter metrics
    chips:
      - Orchestrator Driven
      - Specialized Sub-Agents
      - Every Run Tracked
      - Framework When It Matters

  job_scout_agent:
    visual:
      - job postings into database
      - extract and structure
      - fit score
      - referral path
      - verify and trust
    chips:
      - DuckDB
      - Deterministic
      - Referral-First
      - Agentic Toggle

  adaptive_datagovops:
    visual:
      - abstract adaptive flowing paths
      - minimalist governance motion
    chips:
      - Algorithms
      - Business Rules
      - Custom APIs
      - Optional AI/ML

  document_fingerprinting:
    visual:
      - documents into fingerprint
      - MinHash
      - LSH index
      - distributed cluster
    chips:
      - MinHash
      - LSH
      - Jaccard
      - Dagster Pipeline

  privacy_shield:
    visual:
      - shield
      - PII cards
      - detect / anonymize / reverse anonymize
    chips:
      - Detect PII
      - Anonymize
      - Reverse Anonymize
      - Local-first

  homelab:
    visual:
      - Mac mini
      - Raspberry Pi
      - cloud platforms
      - mesh/tunnel lines
      - containers and services
    chips:
      - Mac mini
      - Raspberry Pi
      - Cloud
      - Docker
      - Tailscale

  elegant_engineers_ai_era:
    visual:
      - elegant engineer core
      - AI engineer ready
      - forward-deployed ready
      - checklists
    chips:
      - Business-first
      - Testing
      - Reliability
      - Security
      - Reuse
```

---

## Prompt template for image generation

Use this structure when calling an image generation model:

```text
Create a professional LinkedIn cover image in exactly {width} × {height} px.

Style:
- {palette_name} palette: {palette_description}
- modern editorial technology cover
- polished, premium, clean, readable
- subtle gradients, glass cards, soft shadows, and balanced whitespace
- no clutter, no tiny unreadable text

Layout:
- left side: category badge, large title, subtitle, optional support line, 3–5 chips
- right side: {visual_metaphor}
- footer: {footer_description}
- keep all important text inside safe margins
- do not crop title or footer
- avoid placing important content at the extreme edges

Text to include:
- Badge: "{badge}"
- Title: "{title}"
- Subtitle: "{subtitle}"
- Support line: "{support_line}"
- Chips: {chips}
- Footer links: {footer_links}

Do not include:
- {must_avoid_text}
- extra company names
- invented product names
- long paragraphs
- unreadable microtext
- distorted logos
- fake UI brand marks

Rendering requirements:
- high-resolution
- sharp typography
- readable at LinkedIn preview size
- clean technical visual metaphor
- final output must be exactly {width} × {height} px
```

---

## Approval workflow

If the user asks to approve the theme before generation, provide a proposal first.

### Proposal format

```markdown
## Proposed cover direction

**Size:** 1279 × 720  
**Palette:** cream_emerald  
**Theme:** Modern data-agent workflow  
**Title:** Job Hunting Is a Data Problem  
**Subtitle:** I Treated It Like One  
**Visual:** Job postings flow into a structured data model, then out to fit score, referral path, verification, and optional agent layer.  
**Footer:** github.com/senthilsweb/ai-agents  

Please confirm, and I will generate the cover.
```

Do not generate the image until the user confirms.

If the user directly says “create now,” “generate,” or “approved,” proceed.

---

## Revision workflow

When revising an image:

1. Preserve what the user liked.
2. Change only what they requested.
3. If they say “previous one was better,” return to that palette/layout and apply only the requested change.
4. If they ask for links to be added, preserve the design and add a footer strip.
5. If they complain about cut-off, reduce text size, increase safe margins, and use the proven `1279 × 720` composition.
6. If they ask for different colors, generate 2 variations using clearly different palettes.
7. Avoid creating a totally new concept unless requested.

---

## Quality checks

Before finalizing, check:

```yaml
quality_checks:
  dimensions:
    required: true
    expected_width: user_or_default_width
    expected_height: user_or_default_height
  readability:
    title_readable: true
    subtitle_readable: true
    footer_readable_if_present: true
  layout:
    title_not_cut_off: true
    footer_not_cut_off: true
    no_overcrowding: true
    safe_margins_respected: true
  content:
    required_title_present: true
    requested_links_present: true
    forbidden_names_absent: true
    no_invented_brand_claims: true
  style:
    palette_matches_request: true
    professional_linkedin_cover: true
```

If any hard check fails, revise once. Do not enter an unbounded revision loop.

---

## Output response

After generation, do not over-explain. Provide either:

```text
Done.
```

or, if files are created outside the image generation UI:

```markdown
Done — here is the generated cover image:

[Download cover image](sandbox:/mnt/data/<file>.png)
```

For non-image generation implementations, include output path, size, palette, and any warnings.

---

## Examples

### Example 1

User:

```text
Create a LinkedIn cover image for my article: "Job Hunting Is a Data Problem. I Treated It Like One." Use subtle green and cream. Add GitHub link at the footer.
```

Extracted cover spec:

```json
{
  "size": "1279x720",
  "palette": "cream_emerald",
  "badge": "AI Agents / Job-Scout Agent",
  "title": "Job Hunting Is a Data Problem",
  "subtitle": "I Treated It Like One",
  "support_line": "Deterministic job search with DuckDB, scoring, referrals, and an optional agentic layer",
  "chips": ["DuckDB", "Deterministic", "Referral-First", "Agentic Toggle"],
  "footer_links": ["github.com/senthilsweb/ai-agents"],
  "visual_metaphor": "job postings flow into a structured data model and out to fit score, referral path, verification, and optional agent layer"
}
```

### Example 2

User:

```text
Create a cover for Adaptive DataGovOps, minimalist, no company names.
```

Extracted cover spec:

```json
{
  "size": "1279x720",
  "palette": "deep_navy_cyan_violet",
  "badge": "Data Governance / Adaptive Operating Model",
  "title": "Adaptive DataGovOps",
  "subtitle": "Data governance needs an adaptive operating model",
  "support_line": "Not one-size-fits-all",
  "chips": [],
  "footer_links": [],
  "visual_metaphor": "abstract adaptive flowing data paths, no labeled boxes"
}
```

### Example 3

User:

```text
Use pink and blue variation. Add LinkedIn and GitHub footer links.
```

Extracted cover spec:

```json
{
  "size": "1279x720",
  "palette": "blue_pink_gloss",
  "footer_links": [
    "linkedin.com/in/senthilsweb",
    "github.com/senthilsweb"
  ]
}
```
