# coda-init

A Claude skill that indexes Coda documents for efficient MCP interaction.

## What it does

When Claude works with a Coda document via MCP, it typically needs 10-15 API
calls just to understand the document structure before doing any real work.
This skill front-loads that discovery into a single indexing step, writing
the results to a `CLAUDE.md` page inside the document — analogous to how
`CLAUDE.md` works in code repositories.

On subsequent conversations, Claude reads one page instead of re-crawling
the entire document.

## How it works

1. Crawls the document: pages, tables, columns, formulas, lookup relationships
2. Detects synced tables (Coda Doc Sync) and traces them to their source
3. Generates a Mermaid ER diagram of table relationships
4. Writes everything to a `CLAUDE.md` page in the document
5. On future visits, reads that single page (2 API calls vs 10-15)

## Commands

```
/coda-init <doc_url_or_name>   Full crawl → create/update CLAUDE.md
/coda-init check               Quick diff against stored index
/coda-init read                Read existing CLAUDE.md
```

## Installation

### Claude.ai (web/app)

Upload `SKILL.md` as a skill in your Claude account or project.

### Claude Code

Copy the `coda-init` folder to your skills directory:

```bash
cp -r coda-init /path/to/your/skills/user/
```

## Requirements

- Coda MCP connector with read+write permissions
- If the document has page locking enabled, the `CLAUDE.md` page must be
  unlocked before Claude can write to it (page options → Locking → unlock)

## Known limitations

- `document_read` does not return tables — the skill must call `page_read`
  on individual pages, which increases the number of API calls for the
  initial crawl
- Page locking is enforced server-side for `content_modify`, contrary to
  Coda's documentation claiming it's client-side only
- Collapsible sections and rendered Mermaid diagrams are not supported by
  Coda's `content_modify` API

See [TODO.md](TODO.md) for planned improvements.

## License

MIT
