<p align="center">
  <img src="screenshots/feature-graphic.png" alt="ChoumarOS — your courses, notes and files in one private place, connected" width="720">
</p>

# ChoumarOS

**Your whole degree, in one place.** A free, private workspace for university students: courses,
lecture notes, files, projects and job applications — connected, searchable, and with an AI
assistant that answers from your own material and shows its sources.

**Try it:** [choumaros.de](https://choumaros.de) ·
[Microsoft Store](https://apps.microsoft.com/detail/9N7BWDMCXT58) ·
Android: [install from Chrome in 30 seconds](https://choumaros.de/android) · Google Play coming soon

> This repository is a public showcase. The application's source code is private.
> Designed, built, tested and operated by [Mohamad Ali Choumar](https://choumar.is-a.dev),
> Software Engineering student at the University of Duisburg-Essen.

<p align="center">
  <img src="screenshots/desktop-01-mission-control.webp" alt="Mission Control: courses, deadlines and projects at a glance" width="49%">
  <img src="screenshots/desktop-04-graph.webp" alt="Knowledge graph: linked courses, notes and files" width="49%">
</p>

## What it does

| | |
|---|---|
| **Mission Control** | What needs you today, what you worked on last, how far each course has come. |
| **Study Hub** | Semesters, courses, credits and grades — read in from a photo of your curriculum, with text recognition running on your own device; only the module names (not the photo) go to an AI for spelling repair, and you review every row before saving. |
| **Capture** | Drop in slides, PDFs, photos or Office files; their text becomes searchable and ChoumarOS suggests where each belongs. |
| **AI Assistant** | Explanations, revision and exam practice grounded in your own notes — every answer cites its sources. |
| **Flashcards** | Spaced repetition: each card comes back when you are about to forget it. |
| **Exams and calendar** | A countdown to your next exams, and your semester exported to any calendar app. |
| **Share with classmates** | Share one course by a read-only link; a classmate can copy it into their own workspace. One click ends the link. |
| **Knowledge Graph** | See how your courses, notes and projects connect. |
| **Three languages** | English, German and Arabic, with full right-to-left layout. |

<p align="center">
  <img src="screenshots/desktop-02-study.webp" alt="Study hub: modules and semester plan" width="49%">
  <img src="screenshots/desktop-05-library.webp" alt="Library: every file and its content" width="49%">
</p>

## Engineering

ChoumarOS is a one-person project held to a team's standard. The numbers below are from the
private repository as of October 2026.

**Architecture**
- Next.js 16 (App Router, Server Components first), strict TypeScript with no `any`.
- Layered: `app/features → application → domain ← infrastructure`; the domain imports no
  framework, database or browser code.
- PostgreSQL is the single source of truth; every untrusted input is parsed with Zod.
- 225 commits since 30 July 2026, about 87,000 lines in 601 files, 25 architecture decision records, 19 migrations.

**Testing — nothing ships red**
- 820 automated tests in 135 files: unit tests plus integration tests against a real PostgreSQL database.
  None skipped.
- 355 browser test runs with Playwright, from 177 test definitions. The full suite runs in Edge; a
  subset (phone layout, accessibility to WCAG 2.2 AA with axe-core, page titles) also runs in
  Firefox and WebKit.
- Every release passes six gates: format check, lint (0 warnings), strict type-check, unit and
  integration tests, browser tests and a production build.

**Security and privacy**
- Row-level security on every table; one central capability policy decides who may do what,
  and missing authority always denies.
- Content-Security-Policy, no secrets in the repository, `npm audit` at 0.
- An internal audit once found a data leak between two accounts; it was closed the same day
  and is now covered by tests.
- Sharing stores only a SHA-256 of each link, never the link itself; links can be stopped at once.
- Hosted in Frankfurt; encrypted daily backups; GDPR account deletion and full export;
  cookieless analytics.

**AI, used responsibly**
- The assistant (Google Gemini) answers only from the user's own data and cites every source;
  semantic search runs on pgvector.
- Retrieved content is treated as untrusted (prompt-injection defence), and the AI can never
  change data.
- If the primary model fails, a second free model and a local engine take over, with simpler
  answers. Without enough evidence in your notes, the assistant says so.

**How it was built**
Most of the code was written with AI coding agents (Claude Code). I defined the product, the
requirements and the priorities, made the product and architecture decisions, tested on real
phones and laptops and reported concrete defects, and approved every production migration and
release. I did not read every line by hand: the result is secured by six checks per release and
my own end-to-end checks. The test suite is the proof — not the model's promise.

<p align="center">
  <img src="screenshots/phone-01-mission-control.webp" alt="Mission Control on a phone" width="28%">
  &nbsp;
  <img src="screenshots/phone-03-course.webp" alt="A course on a phone" width="28%">
</p>

## In three languages

Every screen exists in English, German and Arabic. Arabic is a real right-to-left layout, not a
mirrored afterthought.

<p align="center">
  <img src="screenshots/de/desktop-02-study.webp" alt="Study hub in German" width="49%">
  <img src="screenshots/ar/desktop-02-study.webp" alt="Study hub in Arabic, right to left" width="49%">
</p>
<p align="center">
  <img src="screenshots/de/phone-01-mission-control.webp" alt="Mission Control on a phone, in German" width="28%">
  &nbsp;
  <img src="screenshots/ar/phone-01-mission-control.webp" alt="Mission Control on a phone, in Arabic" width="28%">
  &nbsp;
  <img src="screenshots/ar/phone-04-graph.webp" alt="Knowledge graph on a phone, in Arabic" width="28%">
</p>

All screenshots, per language: [German](screenshots/de) · [Arabic](screenshots/ar).
They come from a test account with invented data — no real student appears anywhere.

## Launch visuals

<p align="center">
  <img src="promo/promo-photo-en.webp" alt="Your semester, one photo away" width="24%">
  <img src="promo/promo-stamp-en.webp" alt="Tested by hundreds of automated tests" width="24%">
  <img src="promo/promo-langs-en.webp" alt="Three languages" width="24%">
  <img src="promo/promo-comic-en.webp" alt="Before and after: a semester in one place" width="24%">
</p>

The same visuals in [German and Arabic](promo).

## Roadmap

Public launch: 27 October 2026.

Shipped in autumn 2026: spaced-repetition flashcards, an exam countdown, calendar export (an
.ics export, not a two-way sync), sharing a course with classmates by a revocable link with
reporting of shared content, and a second free AI model plus a local engine as fallback.

Next:
- Public release on Google Play: after the first request (18 October 2026) Google asked for more
  testing, so a second closed test is running. Until then, Android users can install ChoumarOS
  from Chrome: [choumaros.de/android](https://choumaros.de/android).

## Built with

Next.js · React · TypeScript · PostgreSQL (Supabase) · Drizzle ORM · Zod · Google Gemini ·
pgvector · Playwright · Vitest · axe-core · Vercel (Frankfurt) · PWA ·
Microsoft Store (MSIX) · Google Play (Trusted Web Activity)

## Contact

Questions and feedback: [choumaros.de/support](https://choumaros.de/support) ·
Portfolio: [choumar.is-a.dev](https://choumar.is-a.dev)

© 2026 Mohamad Ali Choumar. All rights reserved.
