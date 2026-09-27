# Duty Rotation Manager — 180 Day

A mobile-first React + TypeScript + Vite duty-rotation application built from the supplied workbook.

## Implemented
- Real 30-staff / 10-duty / 12-rotation baseline from `180_days_duty_rotation_updated.xlsx`.
- 180-day roster represented as 12 × 15-day rotations.
- Main Rotation editor with safe assignment changes.
- Automatic conflict repair by swapping the occupied duty when a safe swap exists.
- Deterministic rebalance/generation engine using eligibility, male-only Evening/Night, previous-rotation repetition avoidance and workload balancing.
- Rule-driven validation: gender, eligibility, minimum gap, repetition, consecutive limits and eligible-duty coverage.
- Live Duty Summary and Staff-wise Rotation derived from the same authoritative roster.
- Repetition analysis.
- Excel import for the workbook's `Staff-wise Rotation` / `180-Day Roster` sheets.
- Excel export recreating six logical views: 180-Day Roster, Staff-wise Rotation, Duty Summary, Checks, Repetition Check, Notes.
- Staff activation/deactivation and eligibility derived from baseline history.
- Configurable rule builder (basic UI) with HARD/SOFT levels.
- Audit log for imports, rebalances and assignment changes.
- Local persistence in browser localStorage.
- Mobile responsive layout.

## Important policy choice
The workbook contains a note about keeping Aakash and Anvita together. That coupling rule is intentionally **not implemented** in this application, per the current requirement.

## Run
Requires Node.js and npm.

```bash
npm install
npm run dev
```

For a production build:

```bash
npm run build
```

## Data model
The Main Rotation is the source of truth. Staff-wise Rotation, Duty Summary, Checks and Repetition are derived views. Editing a roster assignment does not create an independent copy of the roster.

## Current storage
This build is local-first: data is stored in the browser's localStorage. A shared multi-device database/authentication backend can be added later without changing the core rotation engine.

## Additional completion
- Locked assignments: individual roster cells can be locked and the generator preserves them.
- Safer generator: each rotation is solved with deterministic backtracking/matching instead of accepting an incomplete greedy roster.
- JSON backup/restore for moving a complete local configuration between browsers/devices.
- Installable/offline-ready PWA shell via manifest and service worker.
- Assignment changes and restores remain auditable.

### Validation
The constraint engine, baseline roster shape, hard gender constraint, locked-assignment generation, and automatic swap path have been validated independently with TypeScript/Node tests. A full Vite build still requires `npm install`; package installation was timing out in the execution environment, so that final browser bundle step could not be executed here.
