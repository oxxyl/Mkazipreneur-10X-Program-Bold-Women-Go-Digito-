# Mkazipreneur-10X-Program-Bold-Women-Go-Digito-
Data Dashboard for enrollments, outreaches and acceleration activities for the 10x program being implemented by Mkazipreneur in partnership with Outbox, Mastercard Foundationd and UNDCF. BOLD WOMEN GO DIGITO!
[README.md](https://github.com/user-attachments/files/28845688/README.md)
# 10X Program · Bold Women Go Digito — Program Data Summary Dashboard

Interactive single-page data dashboard for the **10X Program (Bold Women Go Digito)**, implemented by **Mkazipreneur Social Enterprise Ltd.** in partnership with **Outbox Uganda, UNCDF and the Mastercard Foundation**.

**Live site:** https://oxxyl.github.io/Mkazipreneur-10X-Program-Bold-Women-Go-Digito-/

---

## What this is

A self-contained `index.html` (no build tools, no backend, no database) that presents program data across **five tabs**:

| # | Tab | Contents |
|---|-----|----------|
| 00 | **Overview** | Program intro, headline KPIs, engagement funnel, enrollment momentum, digital adoption results, outcomes at a glance, district reach, gender, personas |
| 01 | **Foundation Course** | 3,160 enrolled (WEO): districts, enrollment progression, age/education/personas, PWD & refugee inclusion, sectors, digital readiness |
| 02 | **Youth in Work** | 2,513 assessed: earned income / sustained jobs, new jobs created, income distribution, work-conditions improvement, skills retained |
| 03 | **Expression of Interest** | 874 unique MSMEs enrolled via EOI (1,161 applicant records): geography, gender, age, inclusion, founder/employment structure, income by role |
| 04 | **Acceleration** | Journey-to-acceleration funnel (3,160 → 874 → 563 → 500), needs assessment, formalization, finance practices, device & loan demand, business clinics, acceleration achievements |

Data source: the program's June 2026 data reports (Foundation Course/WEO, YIW, EOI, Needs Assessment) plus digital-adoption and acceleration results updates.

---

## Architecture (one file, four parts)

Everything lives in `index.html`:

1. **`<head>`** — Page title, embedded favicon (base64), Chart.js 4.4.1 from cdnjs CDN, Google Fonts (Bricolage Grotesque = headings, DM Sans = body, JetBrains Mono = numbers).
2. **`<style>`** — All design. Colors are defined once as CSS variables in `:root` (`--cyan`, `--gold`, `--navy`, `--teal`, etc.); change a value there and it cascades everywhere. Also contains the motion CSS (card rise-in, tab sheen, funnel steps, reduced-motion support).
3. **HTML body** — Five `<section class="view">` blocks, one per tab. KPI cards use `data-count="…"` attributes for the animated counters. Charts are empty `<canvas>` elements filled by JavaScript. All partner logos are embedded as base64 (no external image requests).
4. **`<script>`** — The engine:
   - **`D = {…}`** — *every number on the dashboard lives in this one object* (`D.ov` overview, `D.f` foundation, `D.y` YIW, `D.e` EOI, `D.n` acceleration).
   - **Helpers** — `barV`, `barH`, `doughnut`, `pie` build standard charts in one line each.
   - **Builders** — `bOverview`, `bFoundation`, `bYiw`, `bEoi`, `bNeeds` wire data to charts; each tab builds lazily on first click.
   - **Motion engine** — IntersectionObserver-based: charts render and animate only when scrolled into view; bars enter with a staggered pop (`easeOutBack`), trend lines draw left-to-right via a custom `lineReveal` clip plugin, doughnuts rotate-scale in, cards/notes rise in with stagger, counters fire on view.
   - **Replay system** — switching back to a visited tab calls `replay(v)`, which re-arms counters, card animations, both funnels, and every chart, so animations play on **every** tab visit, not just the first.
   - **Executive view** — a toggle in the header hides all elements tagged `data-tier="detail"`, collapsing every tab to its headline layer (KPIs, funnels, Venn, defining charts). One file serves two audiences: toggle **off** = full accountability detail for Outbox; toggle **on** = stakeholder summary. To demote a new section to detail tier, add `data-tier="detail"` to its wrapper div.

---

## How to update

### Changing a number
- **Chart values:** edit the `D` object (e.g. `D.y.dist.assessed` = YIW assessed by district).
- **KPI cards:** edit the `data-count="…"` attribute on the card in the HTML (and its label/meta text beside it).
- **Funnels:** Overview funnel = `D.ov.funnel`; Acceleration funnel = `D.n.accFunnel` (each entry: `[value, caption, color, width%]`).

### Changing text
All copy (titles, opening statements, notes, footnotes) is plain HTML inside the five `<section>` blocks — search for the existing wording and edit.

### Deploying
1. Go to: `https://github.com/oxxyl/Mkazipreneur-10X-Program-Bold-Women-Go-Digito-/upload/main`
2. Drag in the new `index.html` (same filename = clean overwrite, no duplicates).
3. Add a short commit message (e.g. "Updated YIW figures") → **Commit changes**.
4. Wait ~1 minute, then hard-refresh the live site (Ctrl + Shift + R).

---

## Data notes & caveats

- **EOI 874 vs 1,161 (not a contradiction):** the EOI tool was designed so applicants could submit details on behalf of their employers or colleagues. **874** = unique MSMEs enrolled through the EOI (the prominent figure, also used in the Acceleration funnel). **1,161** = total individual applicant records captured, which additionally include affiliated individuals such as male founders and over-age founders. EOI-tab charts analyze all 1,161 records.
- **New Jobs Created (153):** based on employment records from EOI data; a full survey is needed for a clearer outlook (footnote shown on the YIW tab).
- **Foundation refugees:** 146 / 4.6% per the detailed nationality table (cover-page rounding may differ slightly).
- Inclusion percentages (PWD/refugee) are reported against program targets at each stage.

---

## Tech summary

- **Stack:** vanilla HTML/CSS/JS + Chart.js 4.4.1 (41 charts) — no framework, no build step.
- **Hosting:** GitHub Pages (deploy from `main` branch, root folder).
- **External requests:** Chart.js (cdnjs) and Google Fonts only; logos & favicon are embedded.
- **Accessibility:** respects `prefers-reduced-motion`; falls back gracefully (content fully visible, no animation) on older browsers without IntersectionObserver.

---

*Maintained by Emmanuel Ogonya (M&E), Mkazipreneur Social Enterprise Ltd. Dashboard built collaboratively with Claude (Anthropic). For program inquiries: Mkazipreneur Social Enterprise Ltd., Kampala, Uganda.*
