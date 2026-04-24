# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A static HTML companion website for the book *The Intent-Driven Enterprise* by Mark Kendall (LearnTeachMaster / Wipro Buildit). 41 self-contained HTML files — `index.html` plus `chapter-01.html` through `chapter-40.html`. No build system, no dependencies, no package manager.

## Running It

Open any file directly in a browser. No server required. External dependency: Google Fonts CDN (Archivo Black, Archivo, JetBrains Mono).

## Architecture

**CSS is duplicated** — each file embeds its own `<style>` block with the full stylesheet. There is no shared CSS file. Changes to styling must be replicated across all affected files.

**CSS variables** (chapter pages):
```
--bg, --panel, --panel2, --border, --black, --dark, --muted
--amber, --amberbg, --amberbdr
--green, --greenbg
```

**Chapter page section structure** (consistent across all 40 chapters):
1. `<header class="header">` — brand + "Chapter N of 40"
2. `.hero` — part tag, chapter number, title, lead paragraph
3. `.section` with "From the Book" — `.book-sections` grid of `.book-sec` items
4. `.section` with "Continued Reading" — `.reading` block
5. `.takeaways` — green checklist panel
6. `.pull-quote` — black panel with amber-accented blockquote
7. `.meta-row` — 3-cell grid (Part / Chapter / Sections)
8. `.nav-row` — Previous / Next chapter navigation (first chapter has `.disabled` on Previous)
9. `<footer>`

**Index page** (`index.html`) uses a different, simpler stylesheet with `.ch-grid` / `.ch-card` components organized by Part sections.

## Book Structure

| Part | Chapters | Title |
|------|----------|-------|
| I | 1–5 | The Breaking Point |
| II | 6–8 | The Shift |
| III | 9–16 | The Core Model |
| IV | 17–21 | Compilation |
| V | 22–27 | The Agentic Platform |
| VI | 28–32 | Architecture in Practice |
| VII | 33–36 | Enterprise Execution |
| VIII | 37–38 | Anti-Patterns |
| IX | 39 | Real Systems |
| X | 40 | The Future |

## Key Patterns

- Mobile breakpoint at `700px` — hero/sections drop to `1.25rem` horizontal padding; meta-row and nav-row stack to single column
- Navigation: each chapter links to the previous and next via `chapter-NN.html` hrefs; chapter 1's Previous cell has `class="nav-cell disabled"`
- The single JS line `window.parent.postMessage({height:...}, '*')` exists for iframe embedding scenarios
