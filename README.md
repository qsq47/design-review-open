# design-review-open

A public-safe Codex skill for UI design review. It compares a design baseline with implementation evidence and helps produce visual-fidelity reports without relying on private company systems or exposing proprietary data.

## What It Does

`design-review-open` helps review UI implementation quality across:

- Layout, alignment, spacing, padding, and responsive behavior
- Typography, line height, font weight, wrapping, and truncation
- Color, opacity, states, and design-token consistency
- Component usage, variants, interaction states, and visual hierarchy
- Icons, fixed assets, charts, illustrations, and evidence annotations
- Full visible-element coverage for stricter final reviews

## Public-Safe Scope

This skill is intentionally generic and does not include company-specific design rules, internal service addresses, private reference content, internal project names, customer data, credentials, or proprietary screenshots.

When creating external reports, it instructs Codex to:

- Generalize confidential project or company names
- Avoid internal URLs, private repositories, account IDs, and credentials
- Treat real text/data differences as content differences unless they affect UI style
- Redact sensitive screenshot content before sharing annotated evidence
- Use public specs, user-provided design files, screenshots, and safe code excerpts as the baseline

## Folder Structure

```text
design-review-open/
  SKILL.md
  README.md
  LICENSE
  .gitignore
  agents/
    openai.yaml
```

## Installation

Copy this folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R design-review-open ~/.codex/skills/
```

Then restart Codex or open a new session.

## Usage

Example prompt:

```text
Use $design-review-open to compare this Figma design with the implementation screenshot and produce a public-safe UI review report.
```

Recommended inputs:

- Figma link, design export, or approved mock screenshot
- Implementation screenshot, local page screenshot, or video frame
- Platform and viewport/device size
- Page state, such as default, empty, error, disabled, selected, or expanded
- Optional public design-system docs or safe code snippets for root-cause analysis

## Report Modes

Concise review:

- Summary and fidelity rating
- Confirmed visual issues
- Needs-confirmation items
- Excluded content/state differences
- Recommended fixes

Strict final review:

- Input inventory and privacy handling
- Page/state pairing matrix
- Baseline sources
- Full visible-element coverage index
- Typography, color, icon, state, and spacing tables
- Annotated evidence images
- Confirmed issue list and self-check record

## Before Publishing Or Sharing

Run a sensitive-content scan before publishing any modified version:

```bash
rg -n "company-name|internal-url|customer-name|credential|secret|token|private-project" design-review-open
```

Do not commit private screenshots, real client reports, internal examples, credentials, or temporary exports.

## License

MIT. See [LICENSE](LICENSE).
