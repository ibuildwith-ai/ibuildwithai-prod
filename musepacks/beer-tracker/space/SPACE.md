# Beer Tracker — space spec

## What it is

A beer journal that learns. The user logs a beer they drank; the space
looks the beer up on the web and breaks it down into its components —
brewery, style, ABV, IBU, hops, malts, yeast, flavor notes with
intensities, and bitterness / sweetness / body / carbonation scores, every
value carrying its source links. The user rates the beer and says what
they liked and didn't like about it, down to individual flavors, and
records where they tried it. Over time the space connects the dots across
all their verdicts — which flavors, hops, malts, styles, and balance
patterns they love and which they avoid — writes a plain-language taste
profile, and suggests real beers to try next, each with a reason tied to
that profile.

## Design (fixed — not a pack question)

It must feel like a real mobile app, not a website: dark theme with an
amber accent, a bottom tab bar with a raised center **Log** button,
bottom sheets for logging a beer and for picking a place, cards with
rounded corners, chips and big Like / Don't-like controls, tap targets of
44px or more, simple and glanceable first with details behind a tap. No
hero section, no wide tables, no desktop layout.

## Surface inventory — FIXED CONTRACT

The tab bar is **exactly these 7, in this order, with these names**:
**Home · Journal · Insights · Log (raised center button) · For You ·
Places · Taste**. No tab may be missing, added, merged, or renamed, and
the Log button sits in the center. `assets/tab-bar-reference.png` in this
pack shows the exact tab bar; the built space is verified against it
(see the pack's verify list). Everything below that is not one of these
7 (for example Where Tried) is a section inside a tab or a sheet — never
an extra tab.

- **Home.** Totals (beers logged, loved count, average rating), recent
  beers, top loved flavor and style, the suggestion count, and one
  rotating unanswered taste question (the question of the day) until all
  8 are answered.
- **Journal.** Every logged beer (`listbeers`), newest first, with
  search and verdict / venue-type filters; tapping a beer opens its full
  detail (breakdown, verdict, venue) with edit and delete.
- **Log (center button).** A bottom sheet: type a beer name → lookup
  auto-fills the breakdown (with a manual-entry path when nothing is
  found) → verdict (love / like / ok / dislike), star rating (1–5),
  would-drink-again, liked / disliked flavor notes (thumbs per flavor),
  free notes, date tried, and the Where Tried section below.
- **Where Tried (part of every log).** Venue type — brewery, restaurant,
  bar, home, friend's place, store, festival, other — plus, when
  `{{venue_lookup}}` is `lookup_and_confirm`, a place search biased to
  `{{home_area}}` that returns real candidate venues with full address and
  coordinates; if several branches match, the user picks the right one
  before saving. When `{{venue_lookup}}` is `manual_only`, or when lookup
  finds nothing, the user types the venue in. **Addresses are never
  invented** — a venue is either a confirmed lookup result or marked
  manual.
- **Insights.** The taste-connection engine: flavor, hop, malt, and style
  affinities (how each correlates with the user's verdicts), balance
  patterns (bitterness / sweetness / body by verdict), and the saved
  narrative taste summary, regenerated on demand from the logs plus the
  taste answers.
- **For You.** `{{suggestions_count}}` suggestions at a time: real beers
  matched to the taste profile, each with a reason tied to the user's
  logged likes and dislikes and source links, plus when they were
  generated and a regenerate action.
- **Places.** Every venue from the logs, aggregated: visit counts, beer
  counts, average rating, venue-type totals, filterable, with the beers
  tried at each place.
- **Taste.** The taste profile tab: the 8 seeded questions with the
  user's answers, editable at any time, plus the generated taste-profile
  summary; answers feed insights, the summary, and suggestions.

## Data model

- `beers` (user's, starts empty): name, brewery, style, description,
  abv, ibu, hops[], malts[], yeast, flavorNotes[{note, intensity}],
  likedNotes[], dislikedNotes[], bitterness / sweetness / bodyScore /
  carbonation (each 1–5 or null), verdict (love | like | ok | dislike),
  rating (1–5 or null), wouldDrinkAgain, serving, notes, triedDate,
  lookupStatus (found | manual), sources[{title, url}], and the venue:
  venueType, venueName, venueAddress, venueCity, venueLat, venueLng,
  placeId, venueManual.
- `taste_questions` (seeded, fixed content): key, question, options[],
  answer (empty at install — answers are the user's own).
- `taste_profile` (generated, starts empty): the narrative summary and
  concrete flavor connections, written by `generatetastesummary`.
- `suggestions` (generated, starts empty): real beers with brewery,
  style, a profile-tied reason, and source links, plus generated-at time.

## Workflow — the rules that make it this space

1. **Lookup before logging.** Logging starts with `lookupbeer`: real,
   sourced component data or an honest "not found" and manual entry.
   Never invent a beer's ABV, IBU, hops, malts, or flavor profile.
2. **The user confirms the place.** Lookup candidates are suggestions
   until the user picks one; chains and same-name venues are exactly why
   the pick is theirs. Never invent an address.
3. **Verdicts drive everything.** Insights are computed from the user's
   own logs grouped by verdict — no generic beer knowledge dressed up as
   personal taste. With very few logs, say the patterns are early.
4. **Suggestions must be real and explained.** Every suggestion is a real
   beer, with a source, and a reason that names the specific logged likes
   or dislikes it connects to. No reason, no suggestion.
5. **Taste questions sharpen, never gate.** The question of the day
   rotates through unanswered questions; the app works fully with zero
   answers, and gets better as answers arrive.

## Actions

The space publishes exactly the actions in `actions.json` (16):
createbeer, updatebeer, deletebeer, getbeer, listbeers, lookupbeer,
searchplaces, gethome, getinsights, generatetastesummary,
generatesuggestions, getsuggestions, getplaces, gettastequestions,
getquestionoftheday, savetasteanswer.

## What is NOT in this space

No creator data of any kind (no logged beers, answers, or suggestions
ship), no social feed, no buying or ordering, no check-in gamification,
and no schedule — everything in it is driven by the user logging a beer.
