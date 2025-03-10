To make Obsidian links functional in GitHub READMEs while hiding metadata, here's the streamlined solution:

### 1. **Fix Obsidian Links for GitHub**

Use **Obsidian Link Converter** plugin ([3]) to auto-convert wiki-links `[[Note]]` → standard markdown `[Note](Note.md)`:

```markdown
# Before

Check [[Important Concept]]

# After

Check [Important Concept](Important-Concept.md)
```

### 2. **Hide Metadata from Rendered Files**

**Metadata Extractor** ([1]) strips YAML frontmatter by exporting metadata to separate JSON files:

```yaml
# Before (visible in GitHub)
---
tags: [demo, test]
---
Content here

# After (metadata stored externally)
Content here
```

### Workflow Setup

1. Install both plugins via Obsidian's community plugins
2. Configure Metadata Extractor to export to `_metadata/` (add this folder to `.gitignore`)
3. Run Link Converter in batch mode before committing changes

This ensures GitHub renders clean markdown with working links.
