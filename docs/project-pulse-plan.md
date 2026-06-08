# Project Pulse Dashboard Implementation Plan

## Objective
Deliver a lightweight, polished, static **Project Pulse** dashboard that shows project status at a glance and runs via VS Code launch config (opening `index.html`, not a directory listing).

---

## Scope / Deliverables
- `app/index.html` — dashboard structure and project card rendering hook points
- `app/styles.css` — polished, responsive styling for dashboard/cards/badges
- `app/project-data.json` — top-level `projects` data source
- `.vscode/launch.json` — **Run Project Pulse Dashboard** launch config serving from `app/` and opening `index.html`

---

## Summary
This plan uses a phased flow: define data + UX decisions first, then implement files with strict ownership, then integrate and validate launch behavior.  
Designer owns UX/UI direction and CSS design decisions; Coder owns implementation and integration, including launch configuration.  
Parallel work is allowed only where file scopes do not conflict.

---

## Work Breakdown by Phase (Ordered Implementation Steps)

### Phase 0 — Requirements Alignment
1. Confirm required fields and UI expectations from project brief.
2. Confirm launch behavior requirements (`app/` cwd + open `index.html`).
3. Lock file ownership boundaries to avoid overlap conflicts.

**File assignments:** none (planning only)  
**Primary owner:** Orchestrator/Planner

---

### Phase 1 — Data Contract + UX Blueprint
1. Define JSON schema for `projects[]` entries:
   - `name`, `owner`, `status`, `recentActivity`, `priority`
2. Define visual mapping rules:
   - status badge treatments
   - priority/risk emphasis
   - card hierarchy and responsive layout behavior
3. Define empty/error display expectations for missing data.

**File assignments:**
- `app/project-data.json` (schema + seed content) — **Coder**
- `app/styles.css` (visual system decisions documented for implementation) — **Designer lead, Coder implement**
- `app/index.html` (semantic structure plan) — **Designer lead, Coder implement**

**Dependency:** Phase 1 must complete before full UI implementation in Phase 2.

---

### Phase 2 — File Implementation
1. Create `app/project-data.json` with valid top-level `projects` array and multiple entries.
2. Build `app/index.html`:
   - exact title: **Project Pulse**
   - links `styles.css`
   - references/loads `project-data.json`
   - renders project cards with class `project-card`
   - shows status, recentActivity, priority, owner, name
3. Build `app/styles.css`:
   - include `.dashboard` and `.project-card`
   - include polished treatment (`border-radius`, `box-shadow`, spacing, readability, responsive behavior)

**File assignments:**
- `app/project-data.json` — **Coder**
- `app/index.html` — **Coder** (with Designer-approved structure)
- `app/styles.css` — **Designer-defined direction, Coder implementation**

**Dependency:** `app/index.html` depends on agreed data shape from `app/project-data.json`.

---

### Phase 3 — Runnable Preview Setup
1. Create `.vscode/launch.json` as strict JSON (no comments).
2. Add config named **Run Project Pulse Dashboard**.
3. Ensure launch:
   - command uses `python3 -m http.server 5500`
   - serves from `${workspaceFolder}/app`
   - uses `serverReadyAction` to open `http://localhost:%s/index.html`
4. Confirm browser lands directly on dashboard frontend, not directory listing.

**File assignments:**
- `.vscode/launch.json` — **Coder**

**Dependency:** Sequential after Phase 2 to validate real UI output.

---

### Phase 4 — Validation + Handoff Readiness
1. Validate file existence and structural checks.
2. Validate UI quality and accessibility baseline.
3. Validate runtime behavior via Run and Debug.
4. Capture any limitations and next steps for final handoff.

**File assignments:** validation across all 4 required files  
**Owners:** Coder + Designer + Orchestrator review

---

## File Assignment Matrix

| File | Primary Owner | Supporting Role | Scope |
|---|---|---|---|
| `app/index.html` | Coder | Designer | Semantic layout, card rendering, JSON reference, required title/content |
| `app/styles.css` | Coder | Designer (lead on UX/UI decisions) | Dashboard visual system, responsive polish, status/priority treatments |
| `app/project-data.json` | Coder | Designer (content clarity feedback) | Valid JSON with top-level `projects` and required project fields |
| `.vscode/launch.json` | Coder | Orchestrator (review) | Deterministic launch config serving `app/` and opening `index.html` |

---

## Role Responsibilities (Designer / Coder)

### Designer
- Define information hierarchy for quick project scanning.
- Specify polished card/badge treatment and responsive layout behavior.
- Ensure readability, spacing, contrast, and accessibility-minded structure.
- Approve visual acceptance criteria for dashboard quality.

### Coder
- Implement `index.html`, `styles.css`, `project-data.json`, and `.vscode/launch.json`.
- Keep behavior deterministic and aligned with schema + UX blueprint.
- Ensure launch config opens frontend page directly.
- Execute validation checks and report issues/risks.

---

## Dependency Graph / Task Dependencies
1. Requirements alignment → required before implementation.
2. Data contract (`app/project-data.json` schema) → required before final `app/index.html` rendering logic.
3. UX blueprint (Designer) → required before final `app/styles.css` polish and HTML hierarchy lock.
4. App files (`app/index.html`, `app/styles.css`, `app/project-data.json`) → required before `.vscode/launch.json` runtime validation.
5. Runtime validation → required before handoff.

---

## Parallelization Plan

### Can run in parallel
1. Initial draft of `app/project-data.json` and initial CSS system draft in `app/styles.css`
   - **Why:** separate files, low coupling at draft stage.
2. Designer UX review and Coder launch-config draft structure
   - **Why:** launch config file is independent of visual styling decisions.

### Must run sequentially
1. Final `app/index.html` render wiring after data schema is fixed
   - **Why:** avoids mismatch between expected and actual JSON fields.
2. Final polish of `app/styles.css` after HTML structure stabilizes
   - **Why:** selector reliability and reduced rework.
3. `.vscode/launch.json` final verification after app files are present
   - **Why:** must verify actual served output opens dashboard page.
4. Acceptance validation after all files are complete
   - **Why:** criteria spans all required files.

---

## Edge Cases to Handle
- `app/project-data.json` invalid JSON syntax.
- Missing required fields (`status`, `recentActivity`, `priority`, etc.) in one or more projects.
- Empty `projects` array (show graceful “no projects” state).
- Unexpected status/priority values (fallback badge style/text).
- Launch opens directory listing instead of `index.html`.
- Port 5500 conflict (document fallback procedure if needed).
- Broken path/reference between `index.html` and `styles.css`/`project-data.json`.

---

## Validation & Acceptance Criteria

### By Coder
- All required files exist at exact paths.
- `app/project-data.json` parses and contains top-level `projects` array.
- Each project includes: `name`, `owner`, `status`, `recentActivity`, `priority`.
- `app/index.html` includes exact title **Project Pulse**, references `styles.css`, references/loads `project-data.json`, and renders `.project-card` entries.
- `app/styles.css` includes `.dashboard`, `.project-card`, `border-radius`, `box-shadow`.

### By Designer
- Dashboard is visually polished (not plain).
- Card hierarchy supports quick scanning.
- Status/priority are visually distinct and readable.
- Layout remains usable across narrow and wide viewport widths.

### By Orchestrator (final acceptance)
- `.vscode/launch.json` includes **Run Project Pulse Dashboard**.
- Launch serves from `app/` and opens `http://localhost:%s/index.html`.
- Running config displays dashboard frontend directly (no directory listing).
- End-to-end behavior matches Project Pulse brief.

---

## Risks / Notes
- Main risk: data/UI contract drift between JSON and HTML render logic.
- Main mitigation: freeze field names before final HTML wiring.
- Main launch risk: incorrect cwd or URL pattern in launch config.
- Keep file ownership strict to prevent Designer/Coder overlap churn.

---

## Open Questions
1. Should status and priority use a fixed allowed vocabulary (e.g., `on-track`, `at-risk`, `blocked`)?
2. Is contributor-friendly summary required in each JSON project object, or only in UI copy?
3. Should `index.html` hardcode starter cards or render entirely from JSON at runtime?
4. If port 5500 is unavailable, should launch config stay fixed (for grading consistency) or support fallback?
