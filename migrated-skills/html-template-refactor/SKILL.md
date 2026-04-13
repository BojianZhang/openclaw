---
name: html-template-refactor
description: Refactor old static HTML/CSS/JS templates into cleaner modern frontend structure without blindly inheriting legacy code. Use when salvaging website templates, extracting reusable sections, simplifying old multi-page HTML themes, modernizing outdated layout structure, or turning legacy template code into cleaner component-oriented rebuild guidance.
---

# HTML Template Refactor

## Goal

Turn old static templates into cleaner rebuild plans.

This skill is for:
- extracting usable structure from legacy HTML templates
- identifying what to keep, rewrite, or discard
- converting template pages into reusable sections or components
- modernizing layout logic without inheriting unnecessary code debt

It is not for blindly polishing old markup line by line.

## Workflow

1. Identify whether the template is worth salvaging.
2. Separate structural value from outdated implementation.
3. Break the template into reusable parts:
   - header
   - hero
   - features
   - portfolio / gallery
   - pricing
   - contact
   - footer
4. Decide what should be:
   - kept as inspiration
   - rewritten from scratch
   - dropped entirely
5. Prefer rebuild guidance, section extraction, and component mapping over direct copy-paste.
6. If the user mainly needs classification or representative sample picking, hand back to `frontend-template-corpus`.

## Read Path

- Read `references/refactor-strategy.md` for the default salvage workflow.
- Read `references/modernization-rules.md` for what to rewrite vs keep.
- Read `references/component-mapping.md` for turning legacy sections into reusable frontend parts.
- Read `references/sample-cases.md` for the strongest sample directions derived from the template pool.
- Read `../frontend-template-corpus/SKILL.md` when the user first needs corpus navigation or template selection.

## Output Expectations

When answering:
1. classify the template value
2. identify reusable sections
3. point out legacy debt and risky code
4. suggest a rebuild order
5. map the template into cleaner reusable frontend pieces

Prefer structural salvage over literal template inheritance.
