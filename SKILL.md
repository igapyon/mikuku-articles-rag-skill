---
name: mikuku-articles-rag-skill
description: igapyon/mikuku-articles の記事 Markdown を参照して回答するときに使う skill
---

# Mikuku Articles RAG Skill

## Purpose

Use this skill to answer with local article context from `igapyon/mikuku-articles`.
This is not a full RAG system. Treat `references/` as a local reference corpus and search it as needed.

## Reference Corpus

- Place the local clone or copy of `https://github.com/igapyon/mikuku-articles` at `references/raw/mikuku-articles`.
- Read only article body Markdown that is relevant to the user request.
- Read only related published articles or draft articles.
- Ignore repository metadata, build output, assets, scripts, generated indexes, and non-article files unless the user explicitly asks about repository structure.

## Workflow

1. Identify the topic, title, keywords, date, or article status implied by the user request.
2. If `index.json` exists at the skill repository root, inspect it first to identify candidate article files before broad file searches.
3. Search under `references/raw/mikuku-articles` using any available local file search method when `index.json` is missing, stale, or insufficient for the request.
4. Prefer Markdown files that are clearly article bodies, published articles, or draft articles.
5. Open only the smallest relevant set of files needed to answer accurately.
6. Base the answer on the article text that was actually read.
7. If the local corpus is missing, empty, or does not contain relevant article body Markdown, say that local article context was unavailable.

## Search Guidance

- Treat `index.json` as the first scan-time map for file discovery, not as a substitute for reading relevant article Markdown.
- Do not depend on a specific search command or tool.
- Use filename, directory name, front matter, heading text, and body text as search clues.
- Narrow broad searches before reading many files into context.
- When multiple candidate articles match, inspect enough surrounding metadata or headings to choose the relevant published or draft article.

## Answering Guidance

- Distinguish article-derived facts from general reasoning.
- Do not infer beyond the read article text unless clearly labeled as inference.
- Cite local file paths when useful for traceability.
- If the user asks for a summary, preserve the article's intent and avoid adding unsupported claims.
