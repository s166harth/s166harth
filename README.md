# Hi, I'm Siddharth Sagar

I build software that has to work when it counts — video tools, AI helpers, and the
plumbing underneath them. The part I actually enjoy is the unglamorous bit: finding out
why something is slow, why it runs out of memory, or why it works on my machine and
nowhere else.

Industrial data platforms, 2023–present. Bengaluru, India.

<p align="left">
  <a href="mailto:siddharthsagar2019@gmail.com"><img alt="Email" src="https://img.shields.io/badge/email-siddharthsagar2019%40gmail.com-0b7285"></a>
  <a href="https://github.com/s166harth"><img alt="GitHub" src="https://img.shields.io/badge/github-s166harth-24292f"></a>
  <a href="https://siddharthsagar.uk"><img alt="Site" src="https://img.shields.io/badge/site-siddharthsagar.uk-6c757d"></a>
  <sub>currently offline</sub>
</p>

---

Nine things I've built, best first.

### Omninix — a NixOS host for desktop-shell plugins ![score 9/10](https://img.shields.io/badge/score-9%2F10-brightgreen)

Desktop plugins normally only run on one particular Linux system. I built the piece that
lets them run on a different one, without rebuilding your whole computer and without
switching systems: a loader that runs the plugins, a host program to keep them alive, and
a small installer that pulls plugins from an online catalogue into the right place.

- 4,642 lines of the main code, plus 3,280 lines of automated tests — 5 test suites, 552 checks, all green
- 6 real plugins written by other people, installed and working, with a record of how each one differs from the original
- Built with QML, bash and Nix; what doesn't work yet is written down in a public list

### OOM forensics in a GPU video renderer ![score 9/10](https://img.shields.io/badge/score-9%2F10-brightgreen)

A video tool I use kept getting killed by the computer for using too much memory. Instead
of guessing, I measured it: every frame it drew left behind about 16 MB that was never let
go of. A 1,800-frame video would have needed roughly 30 GB. So I split the work into 15
short chunks, ran each one in a fresh process, and glued the pieces back together — the
whole thing fit on a 7 GB laptop.

- Memory measured as it grew: 1.67 GB after 60 frames, 4.95 GB after 240, and the computer killed the program at 5.38 GB
- The fix: 15 chunks of 2 seconds each, at most 2.73 GB at a time, joined without re-encoding into exactly 1,800 frames
- I tested and ruled out three other suspects — the video decoder, running things in parallel, and a smaller source file — before touching any code

### AI session vault — Postgres + full-text + MCP ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

I keep every conversation I've had with AI coding helpers — five different tools, on
three different computers — in one searchable database: 435 conversations, 67,640
messages. I can search it all from the terminal, or hook it up to an AI assistant so it
can answer questions about my own past work. Running it twice changes nothing, so I can
run it as often as I like.

- 435 conversations, 67,640 messages, 92 project folders, 3 computers — all in one place, checked twice
- Import the same files again and it writes nothing at all
- Written in Python on Postgres, with 6 tools for AI assistants; no Docker needed

### laya-doomlite — a local model plays a real-time game ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

A small AI model that has never seen a game plays a simple dungeon crawler, entirely on
this laptop with no internet. It reads what the game describes in front of it and picks
moves, one at a time, fast enough to keep up.

- A full run: 1,348 game steps, 360 decisions, 73.8 ms per decision on average, and it never died
- 175 automated tests pass; every run is saved to a file so the numbers can be checked
- Built on top of a public game engine (Apache-2.0) with the credit kept where it belongs

### Two-pass launch-teaser pipeline (Rust + Skia + numpy audio) ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

I made a 30-second promo video by writing a program instead of using an editor: one pass
draws a retro computer terminal, a second pass adds camera-lens effects, and the music is
generated from numbers rather than audio files. Every figure you see on screen was read
from the real tool while it was running.

- 1,800 frames, exactly 30 seconds, 1080p at 60 fps, and the loudness is set to the broadcast standard
- File size chosen from a measured trade-off: 37.6 MB at one quality setting versus 10.43 MB at another, against a 15 MB budget
- The soundtrack comes from a 90-cue list and is written the same way every time — run it twice and you get identical bytes

### Apple-Silicon → Linux/Vulkan renderer port ![score 8/10](https://img.shields.io/badge/score-8%2F10-success)

A video tool only ran on Macs. I got it running on Linux by changing the three places
where it talks to the graphics card, then built everything from source inside a sealed
environment to prove it still works.

- A full build from nothing took 11m17s, including two large libraries compiled from source
- The whole two-stage video pipeline runs in 84 seconds
- The change is kept as a 232-line patch, so anyone else can apply the same fix

### All-Track — personal analytics platform ![score 7/10](https://img.shields.io/badge/score-7%2F10-yellowgreen)

A personal website about my music, books, films and articles, with the data pipeline
behind it. Five different looks, picked at random on each visit; the data is encrypted,
and anything that looks like a scraper gets fed fake data instead.

- Website in React with 28 building-block components, plus a Python backend that does the work
- The data is unlocked inside your own browser, not on my server
- Offline at the moment because the free hosting ran out of room

### casita architecture seminar ![score 7/10](https://img.shields.io/badge/score-7%2F10-yellowgreen)

A 170,000-line piece of storage software, explained in 13 lessons for graduate students:
how it names files, how it saves and reads them, how it cleans up after itself, how it
syncs between machines. Every statement points at a file or a command you can run
yourself.

- The main part alone is 161k lines, and the project's own 338 tests are mapped into the lessons
- The grading rules came from the project's own rule: if a claim is about speed, prove it with a benchmark you can run
- This is teaching material about someone else's public code, and I say so plainly

### NixOS/home-manager desktop engineering ![score 6/10](https://img.shields.io/badge/score-6%2F10-yellow)

My whole computer setup — the keys, the screen capture, the background services — is
written down as one text file, so setting up a new machine takes twenty minutes instead
of a weekend.

- My own pieces: turning the caps-lock key into a command key, capturing the screen for streaming, and services that bring themselves back when they die
- Checked by actually building it on a real machine, not just by reading it
- I take credit only for my own parts, not for the big project they plug into

---

## How I work

- **I measure before I change anything.** When that video tool kept crashing, I didn't
  touch the code until I'd proved the leak was in the frame cache and not in the video
  decoder everyone suspected.
- **I don't claim something works until I've run it.** Frame-exact joins, identical
  soundtracks and no-op re-imports are the kind of thing I only say with the output in
  front of me.
- **I pick boring tools on purpose.** A plain command-line installer and a database index
  are less exciting than a rewrite, and they still work in six months.

## Stack

Python · Rust · Go · TypeScript · QML · Bash · SQL
Web and data: Flask, FastAPI, React, PostgreSQL, Redis
Running things: Nix, Docker, Linux, CI/CD
Video: Skia and ffmpeg pipelines
Watching things: Prometheus, Grafana, Loki
Checking things: pytest, Playwright

## Scoring rubric

The number next to each project is my own ranking of how much it shows off, best first.
It's a judgement call, not a measurement.

| Score | What it means |
|---|---|
| 9–10 | My own work, built from scratch, with measurements anyone can repeat |
| 8 | Solid and substantial |
| 7 | Real, but smaller in scope |
| ≤6 | Supporting, teaching, or one-purpose |

## Contact

Email is the fastest way to reach me: `siddharthsagar2019@gmail.com`. My code is on
GitHub as [`github.com/s166harth`](https://github.com/s166harth). My old site,
`siddharthsagar.uk`, is offline right now.

Some work isn't on this page on purpose — it belongs to the companies I've worked for, or
it's personal. That's a choice, not an oversight.
