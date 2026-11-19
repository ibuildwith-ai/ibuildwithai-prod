# Beer Tracker — Changelog

## 0.6.0 — 2026-11-18
- Every declaration file now ships in the pack, even when empty:
  `connectors.yaml` is back as an empty list (this pack needs no
  account connectors), per the always-present rule (format doc §2,
  format 1.7). A missing declaration file is a structural failure
  at the installer gate — "none" is said explicitly, never by
  omission.

## 0.5.0 — 2026-11-18
- Capabilities split out of connectors.yaml into their own file:
  Places is a built-in Muse capability (no account to connect),
  so it now lives in `capabilities.yaml` with `if_unavailable`
  instead of `if_declined`. The pack needs no account connectors,
  so it ships no `connectors.yaml` at all (format doc §9, format 1.6).

## 0.4.1 — 2026-11-18
- Fix: `used_by` in `connectors.yaml` now names the space by its id
  (`beer-tracker`), not the generic word "space". Component ids
  everywhere — the space's id, skill names, side-chat ids — so the
  installer gate's declared-vs-used cross-check is mechanical
  (format doc §9).

## 0.4.0 — 2026-11-18
- Connectors move to their own file: `connectors.yaml` now declares
  the pack's one optional dependency — the Places capability (venue
  lookup) — with its purpose and its manual-entry fallback. The
  inline declarations in the manifest and in SPACE.yaml are removed:
  one declaration point, per format doc §9 (format 1.1).

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
