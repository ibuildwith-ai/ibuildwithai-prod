# Build the Beer Tracker space (MusePack installer skill)

You are installing a MusePack for your user. The pack's entry file is
`musepack.yaml`; you have already read it (including its
`instructions_for_muse` field) if you are reading this. Follow these steps
in order. Do not skip the interview or the verification.

## 1. Say what you are about to build

In one or two plain sentences: a mobile-app-style space to log beers —
each one looked up and broken down into its components — that learns what
the user likes and doesn't like, connects the patterns, records where each
beer was tried, and suggests real beers to try next. Name anything the
pack will create besides the space (the beer-taste companion skill). This
pack installs **no schedule** by default and requires **no connector**;
the Places connector is optional and only powers venue lookup.

## 2. Check for an existing space first

List the user's spaces. If a space with the pack's slug (`beer-tracker`)
already exists, **do not edit or overwrite it.** Ask the user whether this
is a test install. If it is, build the copy under the slug and name from
`test_install` in musepack.yaml (`beer-tracker-test` /
"Beer Tracker (Test)") so it sits next to the original; it can be deleted
later without touching the original. If it is not a test and the space
already exists, stop and tell the user.

## 3. Ask the pack's questions — only those

Read `questions:` in musepack.yaml. That list is the whole interview: the
pack's creator chose what may be changed, and everything not listed is
fixed — build it exactly as specified and do not ask about it.

- First offer the shortcut: "Want it exactly like the original, or
  customize it?" Exactly-like-original means: take every question's
  default, and ask only the questions marked `required: true` (there is
  no safe default for another person's own home area).
- Ask the questions in the order listed, using the creator's prompt
  wording. For choice questions, present the options from the YAML.
- Keep the answers; each answer replaces the matching `{{placeholder}}`
  in every file you use from here on.
- If the `venue_lookup` answer is `lookup_and_confirm` and the Places
  connector is not available to you, ask the user to connect it before
  building that part — or let them switch to `manual_only`. Never connect
  an account on your own initiative.

## 4. Build the space

Fetch `space/SPACE.yaml` and `space/SPACE.md` (links in musepack.yaml) and
build a full-stack web space from them, with the exact actions listed in
`space/actions.json`. The space needs public web reading at runtime (beer
lookup, taste summary, suggestions) — declare that capability. Apply the
answers from step 3 where the spec marks a `{{placeholder}}`:

- Place searches are biased to `{{home_area}}`.
- Venue entry follows `{{venue_lookup}}` (lookup with user confirmation,
  or manual entry only).
- The For You tab generates `{{suggestions_count}}` suggestions at a time.

The design is fixed and not a question: a real mobile app feel — dark,
amber-accented, bottom tab bar with a raised center Log button, bottom
sheets for logging and place-picking, cards, big tap targets. No hero
sections, no wide tables, no desktop website layout.

## 5. Seed the taste questions — and nothing else

Fetch `space/seed.json` and import the 8 taste-profile questions, with
every answer empty. Create **no** beers, no suggestions, and no taste
summary: the space starts completely empty, ready for the user's first
beer. The pack contains none of the creator's personal data (his logged
beers, taste answers, and generated suggestions are his and do not ship),
and the install must not invent any for the user.

## 6. Install the companion skill

Install the beer-taste skill from `skills/beer-taste/` as a custom skill
for the user, so that when they talk about beers in chat — logging one,
asking why they tend to like a style, asking what to try next — the
conversation follows the same method and uses this space's actions.

## 7. Apply the rules, offer the schedules

Read `rules.yaml` and save its rules (with the user's answers substituted)
as standing instructions for work connected with this space.
Read `schedules.yaml`: every schedule in it is opt-in. Describe each one
in a sentence and create only the ones the user says yes to.

## 8. Verify, then report

Run every check in `verify:` in musepack.yaml against the live space —
actually call its actions (list the taste questions, list beers, run a
beer lookup that saves nothing, run a place search if lookup is on, log a
test beer, check insights, then delete the test beer and confirm the log
is empty again). Report each check as passed or failed with what you saw.
A space that was built but not verified is not installed.

Finish by telling the user, plainly: the space's name and where it sits,
that it starts empty and is ready for their first beer, which questions
they customized versus took as defaults, and anything that failed
verification.
