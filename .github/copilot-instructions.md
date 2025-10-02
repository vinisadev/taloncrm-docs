<!-- .github/copilot-instructions.md
     Concise, actionable guidance for AI coding agents working on this repo.
-->

# Copilot instructions — taloncrm-docs

Goal: help an AI agent become productive editing this Mintlify-based docs site.

## Big picture
- This repository is a Mintlify docs site (see `docs.json`).
- Content is authored as MDX under the repo root (e.g. `index.mdx`, `essentials/*.mdx`, `api-reference/*`).
- API docs are generated from a local OpenAPI spec at `api-reference/openapi.json` (edit that file to change the API reference).
- Static assets live under `images/` and `logo/` and are referenced from MDX/frontmatter.

## Key files to edit (examples)
- Site config: `docs.json` — change site name, colors, navigation. Example: update `"name"` and `"colors"` to change branding.
- Landing and guide pages: `index.mdx`, `quickstart.mdx`, `development.mdx`.
- API spec: `api-reference/openapi.json` — canonical source for API reference pages.
- API topic pages: `api-reference/endpoint/*.mdx` and `api-reference/system/health-check.mdx`.
- AI-tooling docs: `ai-tools/claude-code.mdx`, `ai-tools/cursor.mdx`, `ai-tools/windsurf.mdx`.

## Local developer workflow (concrete commands)
- Install the Mintlify CLI globally if not present:
  npm i -g mint
- Run the preview server from the repository root (where `docs.json` lives):
  mint dev
- Open the local preview at: http://localhost:3000
- If the CLI behaves oddly, update it:
  mint update

## Project-specific conventions and patterns
- Navigation references in `docs.json` use page keys (without `.mdx`), e.g. `"essentials/settings"` maps to `essentials/settings.mdx`.
- MDX files include YAML frontmatter. Follow existing frontmatter keys (title, description). See `index.mdx` and `quickstart.mdx` for examples.
- Reusable UI components (Mintlify components) are used in MDX, e.g. `<Card>`, `<Columns>`. Preserve component props rather than converting to plain HTML when editing examples.
- Images and logo references are relative paths (`/images/...`, `/logo/...`). Keep file names and extensions stable to avoid broken references.
- API docs: `api-reference/openapi.json` is the single source of truth. Do not split API definitions across files; update this JSON and the generated pages will reflect changes.

## Integration points & external dependencies
- Mintlify CLI (`mint`) — used for local preview and dev server.
- Mintlify GitHub app handles deployment from the default branch; pushing to `main` triggers deployment.
- Optional AI tooling: `CLAUDE.md` may be added if using Claude Code (see `ai-tools/claude-code.mdx`). `docs.json` includes contextual options like `chatgpt`, `claude`, `cursor` which indicate integrated tools.

## Common edits and examples an agent may perform
- Change site branding: edit `docs.json` -> modify `name` and the `colors` object.
- Add a guide page: create `essentials/new-topic.mdx` with YAML frontmatter and content using existing components.
- Update API docs: edit `api-reference/openapi.json`; for small textual fixes you may also update `api-reference/endpoint/*.mdx` descriptions.
- Fix a broken image: confirm file exists under `images/` and update the MDX reference to `/images/your-file.png`.

## Debugging hints (observed from repo)
- 404 pages usually mean the navigation path in `docs.json` doesn't match an MDX file. Check `navigation.tabs[*].groups[*].pages` in `docs.json`.
- Local preview problems: ensure `mint` CLI is installed and run `mint update` if outdated.

## Style & content rules to follow (discoverable)
- Keep frontmatter keys consistent (title, description). Match the style and tone used in `index.mdx` and `quickstart.mdx`.
- When editing API reference, prefer changing `openapi.json` over hand-editing generated content.
- Preserve Mintlify MDX components and their usage patterns; follow examples in `index.mdx` (Cards, Columns, AccordionGroup).

---
If anything important is missing or unclear, ask the maintainer which workflow they prefer (e.g., whether API changes should include a changelog entry or automated generation steps).
