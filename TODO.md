# coda-init skill — TODO

## Pending improvements

- [ ] **Page locking behavior**: Coda's MCP currently enforces page locking
  server-side for `content_modify`, contradicting their documentation.
  Monitor for changes — if Coda fixes this (either by respecting account
  permissions or making API writes bypass locks), update Step 5 accordingly.

- [ ] **Collapsible sections in CLAUDE.md**: Coda's `content_modify` API
  does not currently support creating toggle/collapsible headings
  (`blockType` for toggles doesn't exist). When this becomes available,
  use collapsible sections for the Tables list to improve human readability.

- [ ] **Rendered Mermaid ER diagram**: Currently the ER diagram is stored
  as a Mermaid codeblock (readable by Claude, renderable via the Mermaid
  Pack). If `content_modify` adds support for Mermaid formula blocks or
  embedded images, generate a rendered diagram directly on the CLAUDE.md
  page.
