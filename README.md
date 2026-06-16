# mikuku-articles-rag-skill

This Agent Skill reads article Markdown from a local copy of
`igapyon/mikuku-articles`.

## Prepare article data

The article corpus is not committed to this repository.
Clone it under `references/raw/` before using the skill.

```bash
mkdir -p references/raw
git clone https://github.com/igapyon/mikuku-articles.git references/raw/mikuku-articles
```

## Generate index

After preparing the raw article data, generate an index with `miku-indexgen`.

```bash
mkdir -p references/index/mikuku-articles
java -jar ../igapyon-agent-skills/lib/miku-indexgen-1.5.1.jar \
  --input-directory references/raw/mikuku-articles \
  --output-directory references/index/mikuku-articles \
  --title "mikuku-articles index" \
  --markdown
```
