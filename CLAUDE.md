# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static dashboard (`index.html`) that lets DMV office managers see how three staffing/queueing changes would affect customer wait times. The audience is non-technical; `README.md` is written for them and should stay in plain language.

Deployed in two places, both serving `index.html` straight from `main`:
- Vercel: https://dmv-dashboard-omega.vercel.app
- GitHub Pages: https://elenakhtech.github.io/dmv-dashboard/

## Development

No build step, package manager, linter, or tests. Open `index.html` in a browser to run it. Everything (HTML, CSS, JS, data) lives in that one file, with no external dependencies.

## Architecture

- **Results are precomputed, not simulated in the browser.** The `DATA` constant in `index.html` holds output from a C++ simulation of a synthetic 35-customer day (`busy_day.csv`). Neither the C++ code nor the CSV is in this repo. To change the numbers, regenerate them outside this repo and replace the `DATA` literal.
- **Keys encode switch state.** Each `DATA` entry is keyed `a{0|1}f{0|1}r{0|1}` (appointments-first, flexible/cross-trained Vehicle clerk, second Records clerk). All 8 combinations must exist. `a0f0r0` is the "current setup" baseline that every delta is compared against.
- **Per-scenario shape:** `clerks`, aggregate stats (`all`, `appointment`, `walkin`), a `services` array, and a `counters` array. Each stat object has `count`, `avg`, `median`, `longest` and `over` (minutes/people). Counter names change between scenarios (e.g. `Vehicle 2` becomes `Flexible 2`, and `Records 4` is added).
- **Rendering:** `render()` reads the current scenario and redraws the stat tiles, the delta arrows (lower is better) and the two bar charts. `TARGET = 15` is the wait-time goal used for the red line, the yellow "over" bars and the summary text. Adding a new switch means adding a button with a `data-key`, extending `state`/`keyOf`, and supplying data for all new key combinations.

## Rules
- Explain every change in plain language, because the users are non-technical managers.
- Always work on a new branch, never commit directly to main.
- Show me the diff before saving any file.
- Keep README.md up to date when the dashboard changes.
