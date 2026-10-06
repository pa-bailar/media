# Pa' Bailar: images

The flyers and video clips of the events on https://pa-bailar.github.io, and the archive of past events' flyers.
Written by the backend's sweeps (`pa-bailar/backend`, `daily-sweep.yml`), never by hand.

| Folder | What | Kept |
|---|---|---|
| `flyers/` | Each event's flyer, `<post id>-<slide>.webp` | While its event is on the site (until 60 days after its last day) |
| `previews/` | A video's short silent clip, `<post id>-<slide>.mp4` | The same |
| `archive/flyers/` | A small copy of each past event's flyer, for the archive (`data/archive/<year>.json` in the site repository) | For good |

- **How the site uses it:** the site's build (`deploy.yml`, and `ci.yml` for its checks) checks this repository out
  (the latest version only) and copies `flyers/` and `previews/` into its `data/` folder before building. The
  images are served by the site itself, at the same addresses as before; nothing reads this repository at view time.
- **How the sweep writes it:** it copies `flyers/` and `previews/` into its checkout of the site's data, runs, then
  pushes what changed here (new images, and the ones no event uses any more removed), before it opens the site's
  data pull request. Pushes are direct, without pull requests, so old images aren't kept alive by pull request
  references.
- **Size:** it grows with every new flyer (the site repository no longer does). When it gets big, it can be
  recreated with only the current images and the archive, after saving the old full-size images elsewhere.

Details: the backend's `docs/ARCHITECTURE.md` (§10, state and outputs) and the site's `docs/DATA.md`.
