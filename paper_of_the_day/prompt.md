# Paper of the Day

Surface the single most notable AI/ML paper from the last 24 hours.

## Steps

1. **Read** `config.yaml`: `arxiv_categories`, `interests`, `keywords_prioritize`, `keywords_deprioritize`, `max_candidates`, `prioritize_with_code`, `output_format`.

2. **Fetch papers** — stop once you have `max_candidates`. Try in order:
   - **A (preferred):** `https://rss.arxiv.org/rss/<CATEGORY>` — one request per category. Contains today's announced papers.
   - **B (fallback):** Semantic Scholar: `https://api.semanticscholar.org/graph/v1/paper/search?query=<TERMS>&fields=title,authors,abstract,externalIds&limit=20&publicationDateOrYear=<TODAY-2d>:<TODAY>`
   - **C (last resort):** WebSearch `arxiv <CATEGORY> <YYYY-MM-DD> <keyword>`, then fetch `https://arxiv.org/abs/<ID>` for each hit.

   Collect per paper: title, authors, arXiv ID, abstract, date, GitHub URL if any.

3. **Rank**: boost `keywords_prioritize` matches and `interests` alignment; penalize `keywords_deprioritize`; boost code links if `prioritize_with_code`; then rank by novelty, result clarity, and impact.

4. **Pick** the single best paper.

5. **Output** the fields in `output_format` order as Markdown `##` headers:
   - `title` — full title
   - `authors` — full list
   - `arxiv_link` — `https://arxiv.org/abs/<id>`
   - `code_link` — repo URL or "Not released"
   - `why_it_matters` — 2–3 sentences on significance
   - `tl_dr` — one plain-English sentence
   - `key_contribution` — single most important advance
   - `open_questions` — 2–3 questions the paper raises

If nothing is found in the last 24 hours, report the most recent paper found (with date) and suggest broadening categories or keywords.
