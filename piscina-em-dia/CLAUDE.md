# Piscina em Dia — Marketing Workspace

Marketing workspace for Piscina em Dia (https://piscinaemdia.pt), a swimming pool service business in Leiria, Portugal.

- Business context lives in `.agents/product-marketing.md`. Read it before any marketing task. Update it only through the `product-marketing` skill, or when the owner confirms new facts.
- The marketing skills are in the repository root's `.claude/skills/`. They load automatically when Claude Code starts in this folder.
- Write all customer-facing content in European Portuguese (pt-PT), never Brazilian Portuguese.
- Save drafts in `drafts/`. Name each draft by date and channel, e.g. `drafts/2026-11-03-instagram-inverno.md`.

## Rules
- Do not invent company information: no prices, reviews, testimonials, certifications, service area, years in business or customer numbers. If a fact is marked TO CONFIRM, ask the owner.
- Do not claim access to any account (Google Business Profile, Search Console, Analytics, social media, ad platforms) unless it has been connected in the current session.
- Do not publish, schedule, send or spend anything without the owner's explicit approval. Draft only.
