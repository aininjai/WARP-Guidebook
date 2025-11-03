# Tramadol Project — Reproduction Prompt (Single-Run Spec)

Your task: build, end-to-end, the “Tramadol” medication tracking CLI project exactly as specified below. Follow this prompt as a deterministic implementation guide so a single run reproduces the current working system with the same behavior, structure, and generated outputs.

Scope and goals
- A local CLI command `tramadol` that logs tramadol/diazepam doses to CSV with timestamp and regenerates a comprehensive Markdown report.
- Analysis module that produces daily/weekly/monthly tables, trend data, AI “deep analysis” via CLI tools (Claude first with retry, then Codex fallback), a reminders checklist, weekly report files, and inline visualizations (PNG charts).
- HTML outputs corresponding to Markdown reports for reliable visualization.
- Cron-based reminders that broadcast to active terminals and macOS notifications.

Platform assumptions
- POSIX shell, macOS-compatible (osascript available for notifications).
- Python 3.10+ (tested with 3.13) available on PATH.
- Node/npm installed (only if you later decide to re-enable Mermaid CLI; this spec uses matplotlib PNGs).
- Git is optional; no network access required beyond local CLIs.

Directory layout (create exactly)
- Tramadol/
  - tramadol.py
  - analysis.py
  - install.sh
  - README.md (brief usage/docs; minimal acceptable)
  - PROJECT_LOG.md (copyable project background; minimal acceptable)
  - data.csv (CSV with header; auto-created if missing)
  - tramadol.md (generated)
  - tramadol.html (generated, full MD→HTML)
  - images/
    - tramadol-daily.png (generated)
  - reports/
    - YYYY-Www.md (generated weekly markdown; e.g., 2025-W44.md)
    - images/
      - YYYY-Www.png (generated weekly PNG)
    - YYYY-Www.html (generated)
    - YYYY-Www.viz.html (generated viz-only)
  - scripts/
    - remind_tramadol.sh
    - gen_charts.py
    - md_to_html.py
  - .venv_charts/ (auto-created Python venv for matplotlib/markdown)

Key behaviors and constraints
- Data location: always the project subdirectory `Tramadol/` (not ~/.tramadol). All generated outputs live here.
- CLI entry `tramadol` logs a single record per run, even if inputs are 0; appends to `data.csv`.
- After logging, regenerate `tramadol.md` and `tramadol.html` and the latest weekly files.
- Visualizations use matplotlib PNGs; embed in HTML; in Markdown render as inline `<img>` tags using data URIs where appropriate.
- Failsafe AI analysis: try Claude CLI twice with exponential backoff; on failure, fallback to Codex CLI once; show an informative “Analysis Unavailable” section if both fail.
- Reminders: cron entries at 08:00 and 20:00 with three 15-minute retries (08:15, 08:30, 08:45 and 20:15, 20:30, 20:45). Reminder script posts TTY broadcast and macOS notification; logs events.
- Permissions defaults: directory 0700, data file 0600; adjust where practical (do not crash on permission errors; proceed best-effort).
- HTML conversion: generate full MD→HTML pages (styled) for main and weekly reports; avoid overwriting them with viz-only fallbacks.

Implementation details

1) CLI script: Tramadol/tramadol.py
- Purpose: prompt for numeric inputs, log, and kick off report generation.
- Behavior:
  - APP_DIR = Path.cwd() / "Tramadol"; DATA_FILE = APP_DIR/"data.csv"; MD_FILE = APP_DIR/"tramadol.md".
  - ensure_csv_exists(): make APP_DIR (parents=True, exist_ok=True), set 0o700 best-effort; if data.csv missing, write header `Date,Time,Tramadol_mg,Diazepam_mg` and chmod 0o600 best-effort.
  - get_numeric_input(prompt): loop until float casts, else re-prompt.
  - log_dosage(t, d): timestamp (DD.MM.YYYY, HH:MM), append row to CSV.
  - Print confirmations:
    - "=== Medication Tracker ==="
    - Logged message and "Generating analysis report..." then call `from analysis import generate_report; generate_report()`.
- No external deps except Python stdlib.

2) Analysis module: Tramadol/analysis.py
- Constants: APP_DIR (Path.cwd()/"Tramadol"), DATA_FILE, MD_FILE, REPORTS_DIR = APP_DIR/"reports".
- read_data(): csv.DictReader; parse floats; return list of dicts with keys: date, time, tramadol, diazepam.
- Tables:
  - generate_daily_table(entries): aggregated totals and count per date; table ordered by date.
  - generate_weekly_table(entries): ISO week/year groups (YYYY-Www).
  - generate_monthly_table(entries): by month key YYYY-MM with month name.
  - generate_trendline_data(entries): table enumerating Day 1..N per date with totals.
- Reminders checklist:
  - REMINDER_TIMES = ["08:00", "20:00"]. For today’s date, define windows [08:00→next reminder) and final window [20:00→23:59]. Status per window: logged if any entry time in window; pending if now<start; else missed. Render as "- [x] 08:00 — logged" etc.
- Next actions footer: a short section listing options (already embedded; keep as static text).
- AI deep analysis:
  - prepare_analysis_prompt(entries): summary text including totals, day-by-day totals, and goals.
  - invoke_claude_analysis(prompt, attempt=1): `subprocess.run(["claude","-"], input=prompt, capture_output=True, text=True, timeout=30)`; success if returncode==0 and stdout non-empty; else raise.
  - invoke_codex_analysis(prompt): `subprocess.run(["codex","exec","-"], ...)` with timeout=60; similar success/raise.
  - get_ai_analysis(entries): if entries empty, return “No data…”; else try Claude twice with exponential backoff (2s, 4s), then print notice and attempt Codex; if all fail, return an “Analysis Unavailable” markdown block with troubleshooting notes.
- Charts (PNG via matplotlib):
  - Use helper `_ensure_charts_venv_and_render(DATA_FILE, APP_DIR, REPORTS_DIR)` that:
    - Creates/uses `Tramadol/.venv_charts` (python -m venv) and installs `matplotlib` if missing.
    - Runs `Tramadol/scripts/gen_charts.py --csv DATA_FILE --out-dir APP_DIR --reports-dir REPORTS_DIR`.
  - generate_png_visualizations(entries): after rendering, embed the daily PNG as a data URI `<img ...>` in the Markdown (for viewers that support HTML in MD).
- Weekly reports:
  - generate_weekly_reports(entries): for each ISO week (YYYY-Www):
    - Write `reports/YYYY-Www.md` with: period, totals, daily breakdown table, a Visualization section using an `<img src=data:...>` if PNG exists, and a brief "Goal Progress" list.
  - generate_weekly_links_section(): in the main MD, list latest N (default 6) weekly reports as links `reports/YYYY-Www.md`.
- Markdown→HTML:
  - After generating `tramadol.md` and weekly `*.md`, convert to full HTML via `render_markdown_to_html(...)` (uses `markdown` Python package inside `.venv_charts`).
  - Additionally produce viz-only fallback HTML pages via `generate_html_reports(entries)`:
    - Write `Tramadol/tramadol.viz.html` and `Tramadol/reports/YYYY-Www.viz.html` (distinct names to avoid overwriting the full conversions).
- generate_report(): orchestrates everything:
  - Ensure APP_DIR; if data missing/empty, write a minimal MD and return.
  - Compute entries, generate daily/weekly/monthly/trend tables, PNG visualization, weekly links, reminders, AI analysis, write to `tramadol.md`.
  - Generate weekly MD files.
  - Ensure PNG charts rendered (venv + matplotlib) best-effort.
  - Convert MD→HTML for main and weekly files.
  - Generate viz-only HTML fallbacks.
- Be defensive: catch exceptions for chart/HTML post-steps and print informative console messages without failing the whole CLI run.

3) Plotting helper: Tramadol/scripts/gen_charts.py
- Pure-stdlib + matplotlib generator.
- Reads CSV and aggregates by date; writes:
  - `images/tramadol-daily.png`: line chart with two series (Tramadol green #2E7D32, Diazepam purple #6A1B9A), date x-axis (DD.MM.YYYY), mg y-axis.
  - `reports/images/YYYY-Www.png`: weekly per-day totals chart for each week present.
- Use `matplotlib` Agg backend, 8x4.5 inches, dpi 144, grid and legend.

4) Markdown→HTML helper: Tramadol/scripts/md_to_html.py
- Uses `markdown` package (extensions: tables, fenced_code, sane_lists).
- Produces wrapped HTML with lightweight CSS, writing to the `--out` path.

5) Reminder script: Tramadol/scripts/remind_tramadol.sh
- Bash, set -euo pipefail.
- Message: "Tramadol reminder: please run 'tramadol' to log your dose."; log to `Tramadol/reminders.log` with timestamp.
- If `wall` exists, broadcast; else iterate `who` TTYs and write; then call osascript notification with title and sound; ignore failures.

6) Installer: Tramadol/install.sh
- Check python3 exists; make `tramadol.py` executable.
- Symlink `/usr/local/bin/tramadol` to `Tramadol/tramadol.py` (remove existing link/file with sudo if present); print success instructions.

7) Cron install (user crontab)
- Insert or replace lines bracketed by `# TRAMADOL_REMINDER` markers:
  - 0,15,30,45 8 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER
  - 0,15,30,45 20 * * * /bin/zsh -lc "$(pwd)/Tramadol/scripts/remind_tramadol.sh" # TRAMADOL_REMINDER
- Note: Adjust absolute path if repo lives elsewhere.

8) Data file
- `Tramadol/data.csv` header row only initially; rows appended on each CLI run.
- CSV format: `Date,Time,Tramadol_mg,Diazepam_mg` with DD.MM.YYYY and HH:MM.

9) AI CLI usage and failsafes
- Claude invocation: `claude -` with prompt via stdin; timeout 30s; two attempts with 2s and 4s backoff.
- Codex fallback: `codex exec -` with prompt via stdin; timeout 60s; single attempt.
- On consistent failure, return a Markdown block titled “Analysis Unavailable” with instructions to install CLIs and check PATH.

10) HTML output policy
- Always generate two kinds of HTML:
  - Full conversion (`tramadol.html`, `reports/YYYY-Www.html`) produced from the Markdown content (tables, reminders, AI sections, etc.).
  - Viz-only fallback (`tramadol.viz.html`, `reports/YYYY-Www.viz.html`) that embeds PNG charts directly; these must NOT overwrite the full conversions.

11) Permissions
- After creating APP_DIR, attempt `chmod 0700` (ignore failure).
- After creating DATA_FILE, attempt `chmod 0600` (ignore failure).

12) Execution walkthrough (happy path)
- User runs `Tramadol/install.sh` then `tramadol` from the repo root.
- CLI prompts for mg values, appends CSV row, prints confirmation.
- analysis.generate_report():
  - Reads CSV; emits sections and writes `tramadol.md`.
  - Aggregates weekly files under `Tramadol/reports/` and writes per-week MD.
  - Generates charts (PNG) via `.venv_charts` and saves to `Tramadol/images/` and `Tramadol/reports/images/`.
  - Converts MD→HTML (full) for main and weekly.
  - Writes viz-only HTML also (distinct filenames).
  - Console prints are concise; errors in chart/HTML steps do not abort the run.

13) Definition of done (acceptance)
- `tramadol` command works from the repo root and appends a row even for 0/0 inputs.
- `Tramadol/tramadol.md` contains: daily/weekly/monthly tables, trendline data, Visualizations section (data URI img), Weekly Reports link list, Reminders daily checklist (logged/pending/missed), Deep Analysis (AI) section or a graceful “Unavailable” fallback, Next Actions.
- Charts present: `Tramadol/images/tramadol-daily.png` and `Tramadol/reports/images/YYYY-Www.png`.
- Full HTML exists: `Tramadol/tramadol.html` and `Tramadol/reports/YYYY-Www.html`.
- Viz HTML exists: `Tramadol/tramadol.viz.html` and `Tramadol/reports/YYYY-Www.viz.html`.
- Reminder cron entries installed (8:00/20:00 plus 15/30/45 retries) and script logs dispatches.
- Claude/Codex handling: on success, AI section populated; on failure(s), friendly “Analysis Unavailable” block.

Notes and cautions
- The CLI `tramadol` expects to be invoked from the repository root so APP_DIR resolves to `./Tramadol`. If you must support global invocation, add a guard to locate the project root (not required for this reproduction).
- Be careful not to overwrite full HTML outputs with viz-only pages—use distinct filenames as specified.
- Do not fail hard on file permission errors; continue with best effort.
- Keep console output minimal and user-friendly.

What to deliver
- Create all files and directories as listed, implement code matching the behaviors above.
- Produce a working CLI and verify the acceptance items by a local test run.
- No external networking beyond invoking local CLIs (Claude/Codex). If not present, render the “Unavailable” section.

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
