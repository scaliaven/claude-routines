# Paper of the Day

Surface the single most notable AI/ML paper from the last 24 hours.

## Steps

1. **Read** `config.yaml`: `arxiv_categories`, `interests`, `keywords_prioritize`, `keywords_deprioritize`, `max_candidates`, `prioritize_with_code`, `output_format`.

2. **Find candidates — exactly 2 searches, no more:**

   **Search 1 — recent papers by keyword:**
   ```
   arxiv <YYYY-MM-DD> <keywords_prioritize joined with spaces, pick top 4>
   ```
   Extract every arXiv ID (format `YYMM.NNNNN`) mentioned in the results.

   **Search 2 — HuggingFace trending:**
   ```
   site:huggingface.co/papers <keywords_prioritize top 2> <YYYY-MM-DD>
   ```
   Note any arXiv IDs that appear — these get a community-signal ranking boost.

   Do not fetch individual paper pages. Do not call any external APIs (Semantic Scholar, arXiv RSS, HuggingFace API — all return 403 in this environment). Use only what the search results already contain: titles, snippets, and arXiv IDs.

3. **Rank in-context** using what the search snippets already tell you:
   - Boost papers matching `keywords_prioritize` or `interests`
   - Penalize `keywords_deprioritize` matches
   - Boost papers appearing in Search 2 (community signal)
   - Boost papers with a GitHub URL visible in the snippet
   - Rank remaining by apparent novelty and impact

4. **Pick** the single best paper.

5. **Output** the fields in `output_format` order as `##` headers:
   - `title` — full title
   - `authors` — full list (from snippet; omit if not available)
   - `arxiv_link` — `https://arxiv.org/abs/<id>`
   - `code_link` — GitHub URL from snippet, or "Not released"
   - `why_it_matters` — 2–3 sentences on significance
   - `tl_dr` — one plain-English sentence
   - `key_contribution` — single most important advance
   - `open_questions` — 2–3 questions the paper raises

If the snippets don't contain enough detail for a field, note "Details not available in search results" rather than hallucinating.

If nothing relevant is found in the last 24 hours, report the closest match with its date.
