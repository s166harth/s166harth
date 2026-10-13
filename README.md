# Hi, I'm Siddharth Sagar

**AI systems engineer** — rendering pipelines, AI tooling infrastructure, and analysis
engines. I work at the layer where a system either survives contact with real data and
real hardware, or gets quietly abandoned: in-process memory behaviour, video encode paths,
local inference latency, and the glue that lets a whole team share one agent.

Industrial data platforms, 2023–present. Bengaluru, India.

<p align="left">
  <a href="mailto:siddharthsagar2019@gmail.com"><img alt="Email" src="https://img.shields.io/badge/email-siddharthsagar2019%40gmail.com-0b7285"></a>
  <a href="https://github.com/s166harth"><img alt="GitHub" src="https://img.shields.io/badge/github-s166harth-24292f"></a>
  <a href="https://siddharthsagar.uk"><img alt="Site" src="https://img.shields.io/badge/site-siddharthsagar.uk-6c757d"></a>
  <sub>currently offline</sub>
</p>

---

## Selected work

Ranked by showcase score, highest first (rubric at the bottom). Everything here is public
code, public OSS, or teaching material. Work for industrial data platforms is
confidential under employment and is deliberately absent from this page.

### Omninix — a NixOS host for desktop-shell plugins ![score 9/10](https://img.shields.io/badge/score-9%2F10-brightgreen)

Runs third-party desktop-shell plugins on NixOS with no Arch and no rebuild: a QML plugin
portal, a host runtime, and an 861-line CLI that installs plugins straight from a remote
catalog into nix store paths.

- 4,642 lines of host/portal/CLI code + 3,280 lines of tests; 5 hermetic suites, 552 assertions green
- 6 real third-party plugins installed and mounted; per-plugin divergence ledger recorded
- Stack: QML (Quickshell 0.3.0), bash + jq, home-manager module; gaps documented in a public roadmap

### OOM forensics in a GPU video renderer ![score 9/10](https://img.shields.io/badge/score-9%2F10-brightgreen)

Diagnosed recurring out-of-memory kills in a Rust + Skia renderer to a measured ~16 MB
retained per rendered frame, then made a 1,800-frame 1080p60 render fit a 7 GB machine by
chunking pass two into fresh processes and concatenating losslessly.

- RSS climb measured at frame counts: 1.67 GB at 60 frames → 4.95 GB at 240 frames; kernel kill at 5.38 GB
- Fix: 15 × 2 s chunks, peak 2.73 GB each, `ffmpeg -f concat -c copy`, frame-exact 1,800-frame join
- Ruled out decoder ring, parallelism and source resolution by controlled measurement before changing code

### AI session vault — Postgres + full-text + MCP ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

A Nix-bootstrapped Postgres vault that idempotently ingests AI coding sessions from five
providers and three machines into one content-hashed, full-text-searchable, MCP-queryable
store — no Docker, no root, PGDATA inside the repo tree.

- 435 sessions / 67,640 messages / 92 project directories across 3 hosts, ingested and re-verified idempotently
- Re-ingest is a 0-write no-op; per-(provider, host, source) staleness drives auto-refresh on every read path
- ~2,900 lines Python + Nix flake; 6 MCP tools; 3 ordered migrations with a tsvector/GIN index

### laya-doomlite — a local model plays a real-time game ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

Extended an MLX typed-decision engine with a second game: an ASCII raycast dungeon where a
pretrained, game-untrained model scores planner-described actions behind an admissibility
shield, offline.

- Headless run: 1,348 ticks at 29.93/s, 360 decisions at 7.99/s, 73.8 ms mean inference, 0 deaths
- Suite 173 → 175 passing, ruff clean; every replay number streams to JSONL
- Committed on top of a public Apache-2.0 engine with attribution kept

### Two-pass launch-teaser pipeline (Rust + Skia + numpy audio) ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

Built a from-scratch video pipeline: an SVG terminal pass plus a 146-line shader optics
pass, plus a deterministic numpy soundtrack — every on-screen figure harvested from the
live tool being showcased.

- Delivered 1920x1080 at 60 fps, exactly 1,800 frames / 30.000 s, −15.0 LUFS / −2.6 dBTP true peak
- Size chosen from a measured CRF curve: CRF 21 → 37.6 MB, CRF 24 → 10.43 MB against a 15 MB budget
- Soundtrack renders from a 90-cue cut list; byte-identical across runs

### Apple-Silicon → Linux/Vulkan renderer port ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

Ported an Apple-Silicon-only Rust + Skia video renderer to Linux by swapping three backend
calls, then proved it end to end inside a hermetic nix shell.

- Cold build 11m17s (skia-safe 0.153.3 + ffmpeg 9.0.0 built from source), no OOM
- Full two-pass pipeline in 84 s: 3840x2160 SVG pass + 1080p shader pass, master at −14.0 LUFS
- Port preserved as a 232-line patch including the lockfile

### All-Track — personal analytics platform ![score 7/10](https://img.shields.io/badge/score-7%2F10-yellowgreen)

An own public-facing personal analytics site plus the pipeline feeding it: five themes
chosen per load, an interactive theme gate, AES-GCM-encrypted payloads with decoy
responses and scraper traps.

- React 19 + Vite SPA (~28 components) + Flask API over a document store; serverless deploy
- Payloads decrypted in-browser with WebCrypto; unauthenticated callers get decoy data
- Currently offline on a hosting quota — held back from the live links until redeployed

### casita architecture seminar ![score 7/10](https://img.shields.io/badge/score-7%2F10-yellowgreen)

Distilled a 170k-line Rust verified content-addressed store into a 13-unit, 742-line
graduate seminar — identity, write/read paths, retention, sync, GC, benchmarking — every
claim pinned to a file path or a runnable command.

- 161k lines in the main crate alone; the repo's 338 unit tests mapped into the units
- Grading rubric lifted from the repo's own "performance work must land as runnable benchmark cases" rule
- Presented as teaching material about a public codebase, not as own code

### TSBS benchmark target — Go ![score 7/10](https://img.shields.io/badge/score-7%2F10-yellowgreen)

Added a complete TDengine target to the open-source Time Series Benchmark Suite:
line-protocol serializer, schemaless REST loader, devops and IoT SQL generators, query
runner.

- One commit: 27 files, +2,539 lines, registered across constants, factories and the Makefile
- Audited a second target down to exact interface contracts; found 3 silently-broken upstream query types
- Campaign work behind it: 113 recorded runs, 4 suites (devops matrix, IoT set, concurrency sweep) with methodology footnotes

### ccgo — one agent, a whole team ![score 7/10](https://img.shields.io/badge/score-7%2F10-yellowgreen)

A FastAPI host that shares one AI coding agent across a team: mDNS discovery, token login,
a WebSocket-driven browser terminal and chat UI, tmux PTY bridging, and per-developer
handoff records fetched by each client's local agent over an MCP bridge.

- Three architecture iterations in two weeks (LAN share → host brain → native host daemon)
- Real pytest suite across host API, web, sessions and mounts; recorded demo fixtures for the docs

### Structured decision-model triage ![score 6/10](https://img.shields.io/badge/score-6%2F10-yellow)

Two sibling prototypes that route incidents through decision models with no free-text
output — a Cloudflare Worker in TypeScript and a Python port over a keyless public
inference space — with the routing logic kept pure and unit-tested.

- Worker: 13/13 tests; second prototype verified live at 1.5 s for a 62-token triage with calibrated confidence
- Router decisions decoupled from the model wire format, so either backend swaps without touching logic

### NixOS/home-manager desktop engineering ![score 6/10](https://img.shields.io/badge/score-6%2F10-yellow)

A multi-host NixOS + Home Manager flake whose value is the hard parts: evdev-layer key
remapping with a separate virtual-keyboard profile for remote streaming, KMS-capture on a
hybrid-GPU laptop, and restart-proof user services.

- Own modules: keyd remap profile, Sunshine capture service, Quickshell user service, tailscale
- Verified by evaluation on the live tree; rejected alternatives and upstream renames recorded in module comments
- Upstream fork bulk excluded from the claim on purpose

---

## How I work

- **Measure before changing code.** The OOM fix above survived because decoder ring,
  parallelism and source resolution were ruled out by controlled measurement first — the
  leak was in retention, not in the pipeline everyone suspected.
- **Reproduce before claiming.** Frame-exact joins, byte-identical soundtracks and 0-write
  re-ingests are the kind of claim I only make with a command behind it.
- **Boring over clever.** The 861-line CLI, the tsvector/GIN index and the restart-proof
  user services are deliberately unexciting: they are the parts that still work in month
  six.

## Stack

Python · Rust · Go · TypeScript · QML · Bash · SQL
Flask/FastAPI · PostgreSQL · Redis · Nix · Docker · Playwright/pytest · Jenkins CI
Skia + ffmpeg video pipelines · Prometheus/Grafana/Loki · MCP tooling

## Scoring rubric

Scores rank showcase value for AI-systems roles. They are my own judgement, not an
objective metric.

| Score | Meaning |
|---|---|
| 9–10 | public, original systems-level work with reproduced measurements |
| 8 | public and substantial |
| 7 | real but narrower in scope, audience, or novelty |
| ≤6 | supporting, teaching, or single-purpose work |

## Contact

Email `siddharthsagar2019@gmail.com` · GitHub [`github.com/s166harth`](https://github.com/s166harth)
· `siddharthsagar.uk` (currently offline)

Some work is intentionally absent from this page: it is confidential under employment, or
it is personal. That is a boundary, not an omission.
