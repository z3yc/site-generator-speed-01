# site-generator-speed-01

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/z3yc/site-generator-speed-01/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/z3yc/site-generator-speed-01/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A faster drop-in replacement for makefun-site 1.0.0, written from scratch. It is an entry for the [site-generator-speed-01 bounty on make.fun](https://make.fun/bounty/site-generator-speed-01-run-20261122). The output tree is byte-identical to the baseline's for every case: each page's `index.html`, index/tag pages, `build-report.txt` and static files.

## Usage

The entry is `solve.js` plus `main.ts`, Node 22, JavaScript/TypeScript only.

- `main.ts`: the harness driver. It reads `/input/cases.json`, runs `solve.js` on each case, and writes `/output/answers.json`.
- `solve.js`: an ES module exporting `run(input)`. It renders one generated site: Markdown sources with front matter, templates, slugs, reading minutes, tag pages and a build report.

## How it is fast

- Cached slugs with an ASCII fast path.
- A manual HTML escaper (no per-character regex).
- A fused single-pass Markdown renderer with no token objects.
- Front matter parsed without per-line regexes.
- Templates compiled to flat op lists, interpreted into a reused output array.
- Reading minutes counted once per source; per-render-kind variables and scope objects reused.

On the kit's practice set (3 cases) the output is byte-identical to the reference, and `solve.js` runs about 2.8x faster than the baseline (median CPU ~214 ms vs ~597 ms over 10 rounds on the same machine).

## Files

- `solve.js`: the fast implementation.
- `main.ts`: the driver.
- `LICENSE`: MIT.
