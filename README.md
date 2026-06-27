[README.md](https://github.com/user-attachments/files/29400439/README.md)
# Little Luke's BIG Adventure — Trip Dashboard

A single self-contained `index.html` — no build step, no dependencies, no backend.

## Put it on GitHub Pages (~5 minutes)

1. Create a new repo on GitHub (public — GitHub Pages on a free account requires that).
2. Upload `index.html` to the root of the repo (drag-and-drop on the GitHub web UI works fine).
3. Go to **Settings → Pages**.
4. Under "Build and deployment," set **Source: Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
5. Wait ~1 minute, then your link will be live at:
   `https://<your-username>.github.io/<repo-name>/`

## Updating it

Everything that changes week to week — who's confirmed, who's interested in what, checklist content — lives in one block near the top of the `<script>` section, clearly marked:

```
const DATA = {
  ...
};
```

Open the file in any text editor, find that block, change the values, save, and push the updated file back to GitHub (just re-upload it through the web UI, or `git push` if you're working locally). The page recalculates everything else — progress bars, totals — automatically.

A few notes on the data format:
- **Availability**: `true` = confirmed in, `false` = can't make it, `null` = still TBD.
- **Activity interest**: each activity has an `interested: [...]` array of person IDs (`tyler`, `ryan`, `avery`, etc.) — add or remove names there.
- **Checklist items**: just plain strings in an array — add, remove, or reword freely.

Nothing on the page saves visitor input anywhere (no backend = nothing to save to) — the personal cost calculator and the checklist are just in-browser tools for someone to play with on their own, with a "Copy" button to grab their result before they navigate away.

## "My Status" — how people send you their update

There's a tab on the page called **My Status**. Someone picks their name, taps through their availability (cycles TBD → In → Can't on each day), ticks the activities they're into, and answers the +1 question for the segments that allow it. Then they hit **Download My Update**, which saves a `<name>-trip-update.txt` file they send you (Discord, email, whatever).

That file has two parts:
1. A plain-English summary of what they picked.
2. A "ready to paste" line already formatted to match the `DATA.availability` object, plus a one-line note on which activities to add their name to.

So updating the page from one of these files is usually: open the file, copy the bracketed line into `DATA.availability`, add their id to the activity arrays they mentioned, save, push. There's also a **Copy Instead** button if they'd rather paste the text straight into Discord instead of sending a file.

