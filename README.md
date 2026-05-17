# Myth-OS

> A system for interacting with internal signals and presences without triggering resistance.

This repository contains the manuscript, wiki, and companion articles for *Myth-OS*, along with a Jekyll site that renders all of it for the web.

Myth-OS is not self-help, therapy, motivation, or philosophy. It describes how the mind blocks direct access to protected internal states, and how indirect contact with that material is built through structured practice.

## Repository layout

```
.
├── Myth-OS_Book/
│   ├── manuscript/      The book itself
│   │   ├── front-matter/
│   │   ├── part-1-the-problem/
│   │   ├── part-2-the-system/
│   │   ├── part-3-fragmented-systems/
│   │   ├── part-4-advanced-practice/
│   │   ├── part-5-limits-and-long-arc/
│   │   ├── appendices/
│   │   └── back-matter/
│   ├── wiki/            Reference for every system term
│   ├── articles/        Ten-part companion series
│   ├── submission/      Query letter, agent list, submission plan
│   ├── _reference/      Core kernel, outline, writer instructions
│   └── CLAUDE.md        Project guidance
└── docs/                Jekyll site rendering the above (GitHub Pages source)
```

## Reading the source

The manuscript, wiki, and articles are plain Markdown with Obsidian-style `[[wikilinks]]`. They open cleanly in [Obsidian](https://obsidian.md) (the repository includes a vault config under `.obsidian/`), VS Code, or any Markdown viewer.

Start points:

- `Myth-OS_Book/wiki/README.md` — the wiki index
- `Myth-OS_Book/wiki/the-one-sentence.md` — the system compressed to a sentence
- `Myth-OS_Book/wiki/chapters-index.md` — every chapter, appendix, and article in order
- `Myth-OS_Book/manuscript/back-matter/glossary.md` — canonical definitions

## Web site

The `docs/` folder is a Jekyll site that renders the entire body of material with cross-links resolved. See [docs/README.md](docs/README.md) for local build steps and GitHub Pages deployment.

To publish via GitHub Pages: in **Settings → Pages**, set the source to your branch and the folder to `/docs`.

## Working on the text

Conventions for writing and editing are in `Myth-OS_Book/_reference/writer-instructions.md`. The short version:

- Each chapter has one job. Do that job and nothing beyond it.
- Clarity over depth. Concrete over abstract. Function over theory.
- No self-help tone. No motivational language. No solving future chapters early.
- Definitions are canonical. Do not redefine terms across chapters.

## License

All rights reserved.
