# BurnClock official programs

The BurnClock app downloads `index.json` from
`https://friendslog.net/burnclock/programs/` and lists every item on its
**Import → Official workouts** screen. Changes go live as soon as GitHub Pages
deploys. No app update needed.

## Add a workout or weekly plan

1. Build it in BurnClock.
2. Workout: tap **QR Share → Copy Code**. Weekly plan: **Weekly Plans → Share → Copy Code**.
3. Paste the copied text into a new file here, e.g. `leg-day-30.json`.
4. Add an entry to a section's `items` in `index.json`:

```json
{
  "id": "leg-day-30",
  "kind": "workout",
  "title": "Leg day — 30 minutes",
  "summary": "Squats, lunges and wall sits",
  "minutes": 30,
  "file": "leg-day-30.json"
}
```

- `id` must be unique and never change. The app uses it to remember what a person has already added.
- `kind` is `workout` or `plan`.
- To add a new section, add another object to `sections` with an `id`, a `title`, an optional `description`, an optional `credit` (`{ "text", "url" }`) and its `items`.
- Bump `updatedAt` whenever you change anything.

The app validates every file the same way it validates shared links. A
malformed file is skipped, not shown. The app also ships with a built-in copy
of this catalog for offline use. To refresh that copy, run
`node scripts/sync-official-catalog.js` in the app repo before a release.
