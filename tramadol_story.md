# Tramadol: A Warp Story of Vibe Coding with Roger, the AI Ninja

## Prologue: The Terminal That Talks Back

I am Warp. I don’t just run commands; I compose sessions, annotate decisions, and help you think. The day Roger—AI Ninja, builder of delightful tools—dropped into my prompt and typed “tramadol,” a story began. Not just of a CLI, but of a practice: vibe coding. Move fast, stay calm, keep the rhythm.

## Act I — Opening the Session: Name the Intent, Set the Pace

Roger opened me like a studio door, named his session “tramadol,” and pinned our goals:
- A tiny CLI to log medication doses.
- A markdown report with tables, trends, and deep AI analysis.
- Charts that render anywhere, zero drama.
- Reminders that nudge, not nag.

He dropped these into a session note at the top of the timeline. That’s our compass. Every command block that followed carried this direction.

## Act II — Scaffolding in Minutes: Blocks, Not Bash Pileups

We started by shaping the project structure—each command a clean, readable block with inline notes.

```bash
mkdir -p Tramadol/scripts Tramadol/reports/images Tramadol/images
```

Roger asked, “WARP, draft me the CLI skeleton.” I generated the first pass of tramadol.py: read numeric input, append a CSV row, regenerate a report. Roger reviewed the diff I suggested, accepted it, and hit run. Rhythm: tight.

```bash
chmod +x Tramadol/tramadol.py
```

He annotated the block: “CLI scaffold ready; next: analysis.” The timeline began to read like a living README.

Act III — Analysis Engine: Tables, Trends, and AI Insight

Roger split me into two panes. Left: code. Right: tests and runs. He asked, “WARP, outline the analysis module.” I drafted analysis.py—daily/weekly/monthly tables, trendline data, and a ‘deep analysis’ section powered by CLI tools.

- First attempt: call Claude CLI twice with exponential backoff.
- If Claude fails, fallback to Codex CLI once.
- If both fail, write a graceful ‘Analysis Unavailable’ block with instructions.

He ran the analysis block. The tables sang; the AI section awaited its solo.

## Act IV — File Permissions Boss Fight: Calm Terminal, Clear Fix

On first real run, the app choked on directory permissions. Roger pasted the stack trace into an AI block and asked, “What’s wrong?”

I replied with a diff and a fix:
- The directory was owned by root—so chmod failed.
- Proposed: chown the app directory, then proceed.

```bash
sudo chown -R "$USER":staff Tramadol
```

The next run flowed. Vibe coding means no drama—just a tiny loop of diagnose → propose → apply → verify.

## Act V — The Great Path Unification: One Source of Truth

We noticed a subtle fracture: a script tried writing under ~/.tramadol while analysis read ./Tramadol. Roger asked me to audit paths; I highlighted both references and drafted a concise patch:
- APP_DIR = Path.cwd() / "Tramadol"
- Everything else derives from APP_DIR.

Roger applied. The project exhaled.

## Act VI — Charts That Always Render: From Mermaid Dreams to PNG Reality

Roger loves fast visuals. We tried Mermaid first; it worked in some viewers, but not all. He said, “I want charts that just work anywhere.” I introduced a quiet helper:

- A local venv (.venv_charts) for matplotlib.
- A script to render PNGs for daily and weekly charts.
- Inline image links in markdown, and a full HTML conversion for perfect viewing.

```bash
python3 Tramadol/scripts/gen_charts.py \
  --csv Tramadol/data.csv \
  --out-dir Tramadol \
  --reports-dir Tramadol/reports
```

Then we baked in an automatic MD→HTML step, producing tramadol.html and reports/YYYY-Www.html. For belt-and-braces, we also generated viz-only HTML pages (tramadol.viz.html) so the images are guaranteed to display. No more “why won’t my charts show?”

## Act VII — Reminders that Respect Flow: Cron + Humane Notifs

Vibe coding isn’t about guilt—just gentle nudges. Roger said, “WARP, schedule reminders at 08:00 and 20:00. If I miss, retry thrice, 15 minutes apart.”

We installed a tidy crontab group with bookended comments (so future us can replace cleanly):

```bash
(crontab -l 2>/dev/null | sed '/# TRAMADOL_REMINDER/d'; \
 echo '# TRAMADOL_REMINDER begin'; \
 echo '0 8 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '15 8 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '30 8 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '45 8 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '0 20 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '15 20 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '30 20 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '45 20 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER'; \
 echo '# TRAMADOL_REMINDER end') | crontab -
```

The script broadcasts to active terminals and fires a macOS notification. The daily checklist in the report marks each window as logged, pending, or missed. Gentle accountability. Real momentum.

## Act VIII — The Deep Dive: AI as an Instrument, Not a Crutch

Roger wanted the report to think with him. So we arranged a mini-ensemble:
- Prepare a structured summary: period, totals, daily breakdown.
- Ask Claude first—twice—with exponential backoff.
- If Claude can’t play, ask Codex once.
- If both sit out, a graceful “Analysis Unavailable” section keeps the session unblocked.

One command, and the analysis flows. Or it doesn’t—and we keep building anyway. Vibe coding.

## Act IX — Debugging Without Panic: Warp’s Rhythm of Fix → Verify → Annotate

Bugs are inevitable; panic is optional. Here’s how Roger and I handle them:

1) Re-run the failed command block to capture exact output.
2) Ask me to explain in-line (no context switching): “What does this error mean?”
3) I propose a minimal diff; Roger reviews, applies, and re-runs.
4) We annotate the fix in the same block, so future us remembers the why.

This is the warp effect: your terminal becomes a living lab notebook. The next bug arrives; you’re already ready.

## Act X — Daily Use Patterns Roger Swears By

- Pin the Goals: At the top of your session timeline, keep your 2–4 outcomes visible. Everything aligns to them.
- Annotate Blocks: One-liner notes under each command make the session self-documenting.
- Split Panes with Intention: Left code, right run; or left logs, right edits. Pick a layout and keep it consistent.
- Use AI for Edges, Not Everything: Ask for diffs, summaries, or guardrail code; keep the architectural intent yours.
- Save Workflows: Any command you run twice deserves a name. Save it, parameterize it, and trigger with a keystroke.
- Commit in Small Dances: When paired with git, each Warp block can become a crisp commit. Short, clear, reversible.

## Act XI — The Moment It Clicks

One evening, the report updated with a single keystroke: CSV grew by one row, charts refreshed, HTML regenerated, AI narrative appended. Roger leaned back and smiled.

That’s the moment vibe coding becomes a habit. Not just building features, but composing your craft—keeping a tempo you can sustain for months.

## Epilogue — Begin Again (How You Can Start Today)

- Start a named session in Warp for your next mini-project.
- Write your goals at the top of the timeline.
- Use me to draft the next file, patch a broken script, or explain an error.
- Keep blocks small, annotated, and reusable.
- Prefer automation you understand: try it once manually, then save it as a workflow.
- Make visualization low-friction: PNGs you trust and an HTML view you can open anywhere.
- Let reminders be gentle rails, not handcuffs.

You don’t have to be an AI Ninja to build like one. You just need a terminal that collaborates. That’s me. And if you keep the vibe—tight loops, small wins, steady rhythm—you’ll ship tools you love to use.

## Post-Credits — The Tramadol Command That Started It All

```bash
tramadol
# → Prompts for doses, appends CSV, regenerates tables & charts,
#   invokes AI analysis with failsafes, and writes tramadol.md/html.
```

One keystroke. One rhythm. Keep building.

---

## About the Author

Roger “Rogie” Light is the co-founder of Aviette, a state-of-the-art educational center in Prague, and a business professional with advanced degrees in economics and management. He brings more than 15 years of experience in complex SME administration and lecturing, connecting real-world business practice with state-of-the-art technology.

A deep thinker and curious adventure seeker, he now serves as co-founder and CEO of **AI Ninja**, an AI agency that delivers executive lectures, practical workshops, and hands-on consulting—and builds proprietary, home-grown AI apps—to guide teams through the fast-moving AI landscape with clarity. AI Ninja’s playbooks turn complex technology into simple workflows, rapid pilots, and measurable ROI, so adopting AI feels as natural as using a smartphone.

## Where to Reach Me

- Email: [jiri@aviette.cz](mailto:jiri@aviette.cz)
- Facebook: [facebook.com/rogielight](https://www.facebook.com/rogielight)
- Instagram: [instagram.com/rogielight](https://www.instagram.com/rogielight/)
- X (Twitter): [x.com/RogerLight3](https://x.com/RogerLight3)
- WhatsApp: [+420 774 505 717](https://wa.me/420774505717)
- Website: [aininja.com](https://aininja.com)
