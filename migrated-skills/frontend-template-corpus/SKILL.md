---
name: frontend-template-corpus
description: Browse, classify, compare, and extract value from static frontend templates. Use when reviewing HTML/CSS/JS website templates, identifying page patterns, choosing representative samples, grouping templates by use case, or extracting reusable layout and section ideas for redesign or rebuild work.
---

# Frontend Template Corpus

## Goal

Turn large collections of static frontend templates into a usable pattern library. Focus on classification, representative sample selection, section extraction, and practical reuse guidance instead of blindly copying old template code.

## Scope

In scope:
- classifying HTML/CSS/JS templates by site type
- selecting representative samples from a large template collection
- identifying reusable sections such as hero, features, portfolio, blog, pricing, contact, and footer
- comparing templates by structure, not just visual style
- extracting inspiration for redesign, refactor, or rebuild work
- mapping old templates to modern frontend use cases

Out of scope unless directly relevant:
- Java backend architecture
- JVM or database tuning
- publishing or deploying the frontend code itself

## Workflow

1. Identify the template collection and its likely template families.
2. Classify templates by primary use case: corporate, portfolio, blog, product, e-commerce, landing page, industry-specific, admin, and so on.
3. Select representative samples instead of trying to treat every template equally.
4. Identify repeated layout sections and reusable patterns.
5. Distinguish what is worth reusing from what is only outdated decorative code.
6. Prefer structural extraction and pattern reuse over direct copy-paste of legacy HTML.

## When To Read References

Read `references/template-classification.md` when grouping templates by site type.
Read `references/template-classification-001-050.md`, `references/template-classification-051-100.md`, `references/template-classification-101-150.md`, `references/template-classification-151-200.md`, and `references/template-classification-201-260.md` when working with the premium HTML5 template collections.
Read `references/basic-template-classification-yihao-220.md` when working with the lower-quality Yihao 220 simple template batch.
Read `references/mobile-template-classification-017.md` when working with the 17-template mobile or WAP subset.
Read `references/program-backed-mobile-template-notes.md` when a collection includes backend code, admin structure, databases, or CMS-like site logic instead of only static pages.
Read `references/meituan-mobile-fullsite-case.md` for the specific mobile fullsite case based on the Meituan-style package.
Read `references/intelligent-blue-mobile-fullsite-case.md` for the corporate-site-oriented mobile fullsite case with backend structure.
Read `references/sample-selection.md`, `references/top-samples.md`, `references/top-samples-051-100.md`, `references/top-samples-101-150.md`, `references/top-samples-151-200.md`, and `references/top-samples-201-260.md` when choosing representative templates from the premium template pools.
Read `references/basic-top-samples-yihao-220.md` when choosing the best salvageable samples from the Yihao 220 basic-template batch.
Read `references/mobile-top-samples-017.md` when choosing the best representative samples from the mobile-template subset.
Read `references/section-extraction.md` when identifying reusable page sections and layout patterns.
Read `references/examples.md` for concrete output patterns.
Read `references/anti-patterns.md` when guarding against blind reuse of outdated legacy template code.

## Output Expectations

When answering:
1. classify the template or collection
2. explain why the classification fits
3. identify the reusable page patterns
4. recommend representative samples
5. point out outdated or risky legacy parts
6. suggest how to reuse the design without inheriting unnecessary code debt

## Handoff Rules

- If the user asks how to modernize, rebuild, or componentize one chosen legacy template, hand off to `html-template-refactor`.
- If the user asks for hero / CTA / section order / information flow for landing pages, hand off to `frontend-landing-patterns`.
- Keep this skill focused on corpus navigation, classification, representative sample picking, and reusable pattern discovery.
