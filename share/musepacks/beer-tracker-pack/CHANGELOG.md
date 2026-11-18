# Beer Tracker — Changelog

## 0.3.0 — 2026-11-18
- Adds the Beer Chat starter side chat (declared in `side-chats.yaml`):
  a companion chat for talking and researching beer, associated with
  the Beer Tracker space and the beer-taste skill.

## 0.2.1 — 2026-11-18
- Adds the `integrity:` section to the manifest: a SHA-256 hash of
  every file the pack ships, verified by the installer's Quality &
  Safety gate (a mismatch or a missing section stops the install).
- Comment cleanup in `musepack.yaml` and `rules.yaml` (generic
  placeholder wording removed so strict placeholder checks don't
  false-flag).

## 0.2.0 — 2026-11-17
- Surface contract: the space spec now pins the exact tab inventory
  (Home · Journal · Insights · Log · For You · Places · Taste) with a
  verify check and a reference screenshot of the tab bar.
- Privacy fix: the home-area question no longer ships with the
  creator's home area as a default; personal questions carry no
  defaults.
- Slimmed to the data-only format for the universal MusePack
  Installer skill (no instructions inside the pack).

## 0.1.0 — 2026-11-17
- First published pilot: Beer Tracker space spec (16 actions), the
  8-question taste profile seed, and the beer-taste companion skill.
