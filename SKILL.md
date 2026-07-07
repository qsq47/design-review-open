---
name: design-review-open
description: "Public UI design review skill for comparing product designs with implementation screenshots, checking visual fidelity, and producing evidence-based review reports. Use when Codex needs to inspect UI screenshots, Figma or design links, product mockups, implementation screenshots, or frontend/mobile UI code for visual differences, including layout, spacing, typography, colors, icons, states, component usage, and annotated issue reports for external clients or public collaboration."
---

# Public UI Design Review

Use this skill to compare a design baseline with an implementation and report visual fidelity issues for external clients, vendors, agencies, or public collaboration. Keep all output free of proprietary company names, internal URLs, internal tools, private product data, unreleased roadmap details, credentials, and employee or customer information.

## Privacy And Data Safety

- Do not expose private company names, internal project names, internal service URLs, workspace paths, account identifiers, customer data, telemetry, logs, tokens, or credentials.
- Replace confidential names with neutral labels such as `Client`, `Design System`, `Product App`, `Device`, `Feature`, `Module`, or `Internal Knowledge Base`.
- Do not mention or rely on private service endpoints, internal code names, organization-specific repositories, or non-public design-system identifiers unless the user explicitly provides them for this external report and confirms they are safe to disclose.
- When a screenshot contains sensitive text, account data, names, serial numbers, addresses, device IDs, or unreleased copy, either ignore it as content difference or redact it before including annotated evidence.
- Keep source references generic in public deliverables. Prefer `frontend component`, `screen module`, `design token`, or `component library` over internal package or path names unless the user asks for an internal engineering handoff.

## Core Review Principle

Review visual style, not business content. Design mocks and real implementations often use different text, images, data, and localized copy. Treat these as normal content differences unless they affect fixed UI resources or visual behavior.

Count these as visual issues when applicable:

- Fixed UI assets, background artwork, device illustrations, brand assets, or icon glyphs differ from the approved design.
- Text overflows, overlaps, truncates incorrectly, breaks layout, or violates typography styles.
- Charts, gauges, progress indicators, or diagrams differ in geometry, stroke width, scale, spacing, or visual hierarchy.
- Component state, color, enabled/disabled treatment, selected state, hover/pressed state, or error/warning treatment violates the design baseline.
- Layout, spacing, alignment, radius, shadow, elevation, dividers, or container dimensions differ from the baseline.

Ignore by default:

- Status bar content, OS time, battery, carrier, gesture bar, and system safe-area differences unless the product explicitly owns them.
- Absolute vertical offset caused by device chrome, status bar height, dynamic content quantity, localization, or screenshot crop differences unless the design specifies a fixed anchor.
- Real data values, placeholder copy, article titles, product names, image content, or user-generated content when the UI style remains correct.

## Required Inputs

Collect and list available inputs before reviewing:

- Design baseline: Figma node, design export, mock screenshot, design token document, or component spec.
- Implementation evidence: app screenshot, web screenshot, video frame, live URL, or rendered local page.
- Context: product type, screen name, platform, viewport/device size, light/dark mode, language, and relevant state.
- Optional code: frontend/mobile code, component props, style definitions, token usage, or asset files for root-cause analysis.
- Optional constraints: public report, internal engineering handoff, client-facing summary, or annotated evidence requirements.

## Baseline Acquisition Order

Before reviewing, establish the design baseline in this exact priority order:

1. **Figma design and node values first.** If the user provides a Figma URL or node ID, first fetch the exact Figma node screenshot and available Dev Mode-style values before judging issues. Collect layout, size, position, spacing, typography, fill/stroke colors, opacity, radius, shadow/effects, component names, variants, variables/tokens, and screenshot baseline when tools permit. Do not skip this step merely because an implementation screenshot or code is available.
2. **Design specs / knowledge base second.** If Figma cannot be accessed or does not contain the needed values, read available design specifications, component docs, design-token docs, product/category knowledge base, or public design-system rules before generating visual issues. Use these as the secondary baseline and cite them generically in public reports.
3. **Ask before screenshot-only review.** If both Figma and design/spec/knowledge sources are unavailable or insufficient, ask the user whether to continue with an implementation-only risk report. Do not produce a strict fidelity score or confirmed pixel/token defects without a baseline. Mark affected items as `Baseline missing` or `Needs confirmation`.

If a critical input is missing after following this order, proceed only with a clearly stated limitation and never invent baseline values.

## Pairing And State Rules

Before judging visual issues, decide whether the design and implementation are comparable:

- **A-level pairing**: same screen, same platform, same viewport class, same main state, and same relevant sub-state. Confirmed visual issues may be reported.
- **B-level pairing**: same screen but different data, language, content quantity, or minor state variation. Report stable style issues and mark state-dependent items as `Needs confirmation`.
- **C-level pairing**: different screen, major state mismatch, missing matching region, or unclear baseline. Do not count visual issues; provide pairing risks and requested follow-up evidence.

Main state is not enough. Also inspect sub-states such as expanded/collapsed, selected/unselected, enabled/disabled, empty/data state, error/success, loading, and permission-gated visibility.

## Review Workflow

1. Inventory inputs and confidentiality constraints.
2. Pair design and implementation by screen, platform, viewport, and state.
3. Establish the baseline from the user-provided design, public design system, component documentation, or explicit token/spec files.
4. Build a module map: page → section → component → sub-element → visible element.
5. Compare typography, color, spacing, layout, component states, icons/assets, charts, and responsive behavior.
6. Quantify differences where possible using pixels, token names, dimensions, gaps, ratios, color values, or visual diff regions.
7. Check code only when available and needed for root cause: component choice, props, tokens, hardcoded styles, state gates, layout grouping, and asset imports.
8. Produce an evidence-backed report with issue severity, affected visible element, baseline, implementation behavior, root cause, and actionable fix.
9. Include a full visible-element coverage index for final or strict reviews.
10. Redact or generalize sensitive content before sharing externally.

## Minimum Granularity

For strict reviews, every visible item must be traceable by a user-facing name.

- Use visible names for text, controls, icons, containers, charts, dividers, and spacing relationships. Examples: `Back arrow`, `Primary action button`, `First card background`, `Status label`, `Right chevron`, `Empty-state illustration`.
- Abstract names such as `Title#1`, `cardContainer`, `trailing`, or `Layer 23` may be included only as secondary identifiers.
- Text content differences are not UI issues by themselves, but each text element still requires typography, color, alignment, line-height, wrapping, and spacing checks.
- Passing items should appear in the coverage table, not only failing items.
- If an element is not listed in the coverage index, do not claim full coverage.

## Baseline Priority

Use the strongest available baseline in this order:

1. User-provided review instructions or public client design specification.
2. Figma node data, component instances, variables, Dev Mode values, or explicit token bindings.
3. Public or user-provided design-system component and token documentation.
4. Source code evidence of implemented components, props, token references, hardcoded styles, and state logic.
5. Design and implementation screenshot measurement, sampling, overlay, and visual diff.
6. General UI design judgment.

Do not call a screenshot-sampled value a design token. Only call something a token when the design, spec, or token file explicitly names it.

## Component And Token Rules

When multiple components or tokens could apply, output a candidate table before concluding.

Candidate table fields:

| Element | Candidate component/token | Evidence | Selected baseline | Confidence | Needs design confirmation |
|---|---|---|---|---|---|

Decision rules:

- Explicit Figma component, variable, or token binding beats inferred component semantics.
- Component semantics narrow the token type but do not automatically determine a color family.
- Product theme, brand theme, page context, and state determine final token variants when provided.
- Special semantics such as destructive, warning, success, disabled, link, ghost, and subtle states override generic primary-action styling.
- If the baseline is ambiguous, mark `Needs confirmation` rather than forcing a pass or fail.

## Typography Checks

For every visible text element, inspect:

- Font family or system font usage.
- Font size, weight, line height, letter spacing, color, opacity, and text style token.
- Alignment, width, wrapping, truncation, max lines, and overflow behavior.
- Relationship to neighboring icons, labels, values, and containers.
- State-specific treatment for disabled, selected, error, warning, success, placeholder, and helper text.

## Color Checks

Judge colors in two steps:

1. Verify semantic/token correctness: target token, component role, state, and theme.
2. Verify final rendered color: token value, opacity, overlays, parent opacity, disabled blending, image tint, and screenshot sampling.

Color table fields:

| Element | Target token/value | Source token/value | Opacity/alpha | Final rendered value | Screenshot sample | Conclusion |
|---|---|---|---|---|---|---|

Do not mark color as passing merely because a token name appears in source code. Calculate or reason through final visual output when opacity, tint, overlay, or disabled treatment is involved.

## Icon And Asset Checks

Every visible icon or fixed asset must be checked independently:

- Asset source: design-system icon, public icon library, local SVG, PNG/WebP/JPEG, or generated asset.
- Glyph shape, orientation, size, stroke/fill width, visual center, and bounding box.
- Color token, state token, opacity, disabled treatment, and contrast.
- Whether the icon is decorative, navigational, semantic, functional, or status-related.
- Whether filename, usage, and actual glyph match.

Icon table fields:

| Visible icon | Component/location | Asset source | Actual glyph | Target glyph/icon | State | Target color | Implemented color | Conclusion |
|---|---|---|---|---|---|---|---|---|

Open and inspect local SVG/path assets when available. Do not assume an icon is correct from filename or code comments alone.

## Layout, Spacing, And Container Checks

Inspect these at page, module, component, and sub-element levels:

- Page background, scroll behavior, safe area, top/bottom bars, and fixed regions.
- Section order, module visibility, section title styling, and section-to-content gap.
- Card/container width, height, padding, border, radius, shadow, elevation, and background.
- Row height, list item alignment, divider inset, chevron placement, and touch target size.
- Grid, two-column, flow, masonry, and responsive wrapping behavior.
- Horizontal and vertical gaps between text, icons, controls, cards, and modules.

For two-column or flow layouts, check row completeness:

- Half-width items should pair correctly unless the design explicitly allows a single half-width item.
- If filtering or feature gating hides one item, verify the remaining item expands, reflows, or has an approved empty state.
- Report visible empty half-columns, isolated cards, broken rows, or unbalanced grids as layout issues unless explicitly approved.

## State And Interaction Visual Checks

Check state combinations, not only isolated states:

- Enabled, disabled, selected, unselected, active, inactive, pressed, hover, focused, loading, warning, success, and error.
- Combined states such as `selected + disabled`, `unchecked + disabled`, `active + unavailable`, and `loading + disabled`.
- Whether text, icon, background, border, shadow, and control affordance all reflect the same state logic.
- Whether unavailable features are hidden, disabled, or shown as navigable according to the provided baseline.

If business availability is unknown, mark state-dependent differences as `Needs confirmation`.

## Evidence Images

For final reports, provide visual evidence for each confirmed issue using this mandatory format:

- Create **one image per issue**. Do not use a single overview image as the only evidence for multiple issues.
- Use a side-by-side comparison image whenever a design screenshot is available: **left = design baseline**, **right = implementation**.
- Add a title above the image such as `Issue 2: active blue token mismatch`.
- Above or near the left/design side, label the correct design information, for example `Design: Figma token accent/... #29A9FF`, `Design: width 360px`, or `Design: radius 24px`.
- Above or near the right/implementation side, label the implemented information, for example `Implementation: source rgba(40,116,254) / sampled #367BF8`, `Implementation: screenshot height 88px`, or `Implementation: component prop disabled=false`.
- Use exact values whenever Figma Dev/node data, design tokens, component specs, source code, or implementation tokens provide exact values. Do not write `approx`, `about`, `roughly`, `around`, `视觉约`, `大约`, or `约` for those values.
- Use screenshot sampling values only as secondary evidence when exact source/design values are unavailable or to explain rendered anti-aliasing. Label them explicitly as `sampled` / `截图采样`, not as the source of truth.
- If exact Figma and code values conflict with sampled screenshot colors or sizes, report the exact Figma/code values first and mention sampling only as supporting evidence.
- Draw red boxes around the affected element on both the design side and implementation side when both counterparts exist.
- Use red fine outlines, issue number badges, pointer lines, and outside note areas when useful, but avoid covering the UI being reviewed.
- Use a dark or neutral header band above the screenshot crops for the issue title and measurement labels, matching the provided reference style when possible.
- Keep comparison crops visually aligned: use the same viewport scale, same crop bounds, and same element position whenever possible. If screenshots have different pixel densities, resize the implementation to the design screenshot's logical size before cropping.
- The image title and both side labels must be fully readable. **Do not allow label text to be clipped, truncated, overlapped, or broken mid-word / mid-token.** Increase canvas width, header height, or font size/line height as needed.
- Wrap long labels only at natural boundaries such as spaces, punctuation, `/`, `:` or `→`; never split hex colors, token names, file names, numbers with units, or CSS/RN values across lines.
- If a label is still too long, shorten it semantically while preserving the key design value and implementation value, then put the full detail in the issue block text below the image.
- Keep at least 12px padding around title/label text and at least 16px spacing between the left and right panels so text and red boxes do not collide.
- Use red boxes only for the actual differing element, not the whole screen, unless the whole container is the issue.
- Save evidence images with stable names such as `issue-01-short-title.png`, ordered the same as the report. Prefer PNG output at a readable document width; when embedding in collaborative docs, use a width around `760` unless the document layout requires otherwise.
- For repeated issues, still provide one representative side-by-side image and list all affected locations in the issue text.
- If no design screenshot is available but a spec/token baseline exists, create a comparison image with a left-side spec/token panel and right-side implementation crop.
- If neither design screenshot nor spec/token baseline exists, do not create a fake comparison image. Ask whether to continue with a risk report; if the user agrees, mark evidence as `Baseline missing` / `Needs confirmation`.
- For token/spec not found, annotate the affected element and mark it as `Spec not found`, not as a confirmed visual bug.

Markdown image format:

```markdown
![Issue X: concise caption](/absolute/path/to/annotated-image.png)
```

Collaborative-document image format when supported:

```markdown
<image url="file:////absolute/path/to/annotated-image.png" width="760" align="center" caption="Issue X: concise caption"/>
```

## Report Structure

For a concise review, include:

1. Summary and overall fidelity rating.
2. Input inventory and pairing confidence.
3. Confirmed visual issues grouped by severity.
4. Needs-confirmation items and excluded content/state differences.
5. Recommended fixes.

For a strict final review, include these sections in order:

1. Input inventory and privacy handling.
2. Page/state pairing matrix.
3. Baseline acquisition record, sources, and token/component references.
4. Overall score and issue counts.
5. Full visible-element coverage index.
6. Typography review table.
7. Color/token review table.
8. Icon/asset review table.
9. State and interaction visual review table.
10. Layout/spacing/container review table.
11. Per-issue side-by-side comparison evidence images.
12. Confirmed issue list.
13. Needs-confirmation, risk, and coverage gaps.
14. Content/state differences excluded from UI issue count.
15. Final self-check record.

Allowed coverage conclusions:

- `Pass`
- `Confirmed issue P0/P1/P2/P3`
- `Needs confirmation`
- `Coverage missing`
- `Content/state difference excluded`

Do not use vague conclusions such as `basically consistent`, `looks close`, or `checked`.

## Issue Severity

- **P0 / Critical**: Blocks main flow or severely breaks visual structure, such as missing primary action, wrong navigation hierarchy, broken layout, unreadable text, severe overlap, or incorrect critical state color.
- **P1 / High**: Highly visible and impacts user trust or product quality, such as wrong fixed asset, wrong icon glyph, major spacing/layout deviation, wrong selected/disabled state, or primary CTA token error.
- **P2 / Medium**: Noticeable fidelity issue that does not block use, such as 4px+ key spacing deviation, font weight mismatch, card padding mismatch, chart geometry mismatch, or incorrect non-critical token.
- **P3 / Low**: Minor polish issue, such as tiny radius mismatch, slight local offset, subtle opacity difference, or non-critical shadow mismatch.
- **Needs confirmation**: Baseline/state/data/spec is unclear. Do not count as confirmed visual issue.

## Fixed Issue Block Template

```markdown
#### X. Issue title using a visible element name

![Issue X: side-by-side design vs implementation comparison](/absolute/path/to/comparison-image.png)

- **Severity**: P0 / P1 / P2 / P3 / Needs confirmation
- **Dimension**: Color / Typography / Spacing / Radius / Layout / Hierarchy / Icon / Asset / Chart / State
- **Location**: Specific visible location in the screen
- **Baseline**: Design token, component spec, Figma value, public design-system rule, or visual baseline
- **Implementation**: What the implementation currently shows
- **Quantified difference**: e.g. `gap 12px vs 8px`, `height -4px`, `dx +5px`, `target #000000CC vs rendered #00000099`. Use exact Figma/code/token values when available; use approximate language only when the value comes solely from visual estimation or screenshot sampling.
- **Component/token check**: Whether the correct component, variant, state, and token are used
- **Root cause**: Component choice, prop, token, layout rule, state gate, asset mismatch, hardcoded style, or unknown
- **Recommendation**: Actionable fix for design or engineering
- **Status**: Confirmed issue / Needs confirmation / Spec conflict / Excluded content difference
```

## Self-Check Before Delivery

Before calling a strict review complete, verify:

- Figma design screenshot and node values were attempted first when a Figma link/node was provided.
- If Figma was unavailable, design specs / knowledge base / design tokens were checked before screenshot-only review.
- If no baseline existed, the user was asked whether to continue and the report avoids strict fidelity scoring.
- Pairing level and state assumptions are stated.
- Every visible element appears in the coverage index.
- Text, icons, state, spacing, and containers are checked separately.
- Confirmed issues have evidence, severity, baseline, implementation behavior, measurement, and recommendation.
- Each confirmed issue has exactly one primary comparison image, preferably side-by-side with design on the left and implementation on the right.
- Each comparison image labels both the design-correct information and implementation information, and red-boxes the affected element.
- Evidence image titles and labels are readable with no clipping, overlap, truncation, or broken mid-token text.
- Exact Figma Dev/node values, design-token values, component-spec values, and source-code values are reported without approximate wording such as `约`, `大约`, `around`, or `roughly`.
- Screenshot sampling or visual-estimate values are explicitly labeled as such and are not presented as source-of-truth values.
- Needs-confirmation items are not counted as confirmed issues.
- Pure content/data differences are excluded and listed separately.
- Sensitive names, internal URLs, private tool names, credentials, customer data, and unreleased details are removed or generalized.
- Any annotated images are readable and do not expose sensitive data.

## Special Cases

- If the user provides a public design-system or token document, use it as the baseline and cite the relevant component/token names.
- If only two screenshots are available, perform a visual comparison and clearly mark token/component claims as unavailable.
- If implementation code is available, provide root-cause hypotheses and file-level references only when appropriate for the audience.
- If the report is client-facing, avoid internal jargon and focus on visible impact plus recommended fix.
- If the report is engineering-facing, include component, prop, token, and layout details when safe to disclose.
- If the user corrects a false positive, update the issue count, severity, and report text rather than only acknowledging it in chat.
