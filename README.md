# Faster makefun-site

A drop-in replacement for make.fun's makefun-site 1.0.0 static site generator that returns exactly
makefun-site's answer for every case — the same output tree, byte for byte — in less CPU time.

- `main.ts` is the harness driver: it reads `/input/cases.json`, answers each case with `run`, and writes
  `/output/answers.json`.
- `solve.js` is the entry: a dependency-free ES module whose `run(input)` builds one site's output tree.
  It implements makefun-site's own front matter, permalink, Markdown, template and report rules, with the
  hot paths rebuilt for speed: inline Markdown copies plain runs in single slices instead of escaping
  character by character, block lexing classifies lines by their first characters instead of stacked
  regexes, slugs are memoised within a build, and templates are compiled once into straight-line
  JavaScript functions instead of being walked node by node for every page.
