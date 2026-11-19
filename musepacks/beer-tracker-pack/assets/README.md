# Assets

This pack ships **one image file**:

- `tab-bar-reference.png` — a screenshot of the creator's tab bar
  (Home · Journal · Insights · Log · For You · Places · Taste). It is
  part of the space's fixed surface contract: the installer builds the
  tab bar to match it and verifies against it. It shows empty UI chrome
  only — no user data.

No other images ship. The space itself has no beer photos, label art, or
venue images in its data model — a beer's record is its sourced component
breakdown and the user's verdict, and a venue's record is its confirmed
name, address, and coordinates. If a future version of the space adds
label images, they would be fetched per beer at lookup time (with
sources), never shipped as pack assets.
