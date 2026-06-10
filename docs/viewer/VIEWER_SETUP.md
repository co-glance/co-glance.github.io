# Dataset Viewer — Adding to an Existing GitHub Pages Site

---

## What's in the `viewer/` folder

```
viewer/
  index.html                    ← the viewer app
  frames/
    runs.json                   ← list of available runs (used by the dropdown)
    04-13_run_1_Clean/
      rgb_0000.webp             ← pre-rendered RGB composites
      gt_0000.webp              ← pre-rendered GT BBox composites
      ...
      metadata.json
    03-30_run_1_Clean/
      rgb_0000.webp
      gt_0000.webp
      ...
      metadata.json
```

---

## Step 1 — Clone your existing repo

If you don't already have the repo checked out locally:

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

---

## Step 2 — Copy the viewer files into the repo

Copy the entire `viewer/` folder into your repo's `docs/` directory:

```bash
cp -r /path/to/provided/viewer docs/viewer
```

Your repo's `docs/` folder should now look like:

```
docs/
  index.html              ← your existing site homepage (unchanged)
  ...                     ← your other existing pages (unchanged)
  viewer/
    index.html            ← the dataset viewer
    frames/
      runs.json
      04-13_run_1_Clean/
      03-30_run_1_Clean/
```

---

## Step 3 — Commit and push

```bash
git add docs/viewer/
git commit -m "Add dataset viewer"
git push
```

The `frames/` files are ~30 MB total across both runs, so the push takes
20–60 seconds on a normal connection.

> If `git push` asks for credentials, use your GitHub username and a
> [personal access token](https://github.com/settings/tokens) (not your password)
> as the password field.

---

## Step 4 — Open the viewer

GitHub Pages redeploys automatically within 1–2 minutes of the push.
The viewer will be live at:

```
https://<your-username>.github.io/<your-repo>/viewer/
```

You'll see the aerial + ground composite image with the satellite GPS map
overlaid in the top-left corner. Use the **run dropdown** to switch between
datasets, the **slider** or **← → arrow keys** to scrub through frames, and
the **RGB / GT BBox** buttons to switch modalities.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Page loads but image is blank | Open browser console (F12). A `runs.json` 404 means `docs/viewer/frames/` wasn't pushed — run `git status` to confirm the files are committed. |
| GitHub rejects the push | Run `git diff --cached --stat` before committing to confirm only `docs/viewer/` files are staged. |
| Viewer shows a 404 | Wait another minute and hard-refresh (Ctrl+Shift+R). Deploys can take up to 5 minutes. |
| GT BBox button is greyed out | Normal — means that modality wasn't included in the export for that run. |
