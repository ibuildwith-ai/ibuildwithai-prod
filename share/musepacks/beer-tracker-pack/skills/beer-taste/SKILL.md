# Beer taste

Use this skill whenever the user talks beer in connection with their Beer
Tracker space: logging a beer from chat, asking why they tend to like or
dislike something, or asking what to try next.

## Logging from chat

1. Run the space's `lookupbeer` with the beer's name first. Use the
   returned breakdown — brewery, style, ABV, IBU, hops, malts, flavor
   notes, balance scores — and keep its source links on the record. If
   the lookup finds nothing, say so and offer manual entry; never fill
   the breakdown in from general knowledge without a source.
2. If they say where they tried it and their pack's venue mode is
   lookup-and-confirm, run `searchplaces` (biased to their home area) and
   let **them** pick the venue from the candidates. Never invent an
   address, and never pick a branch for them.
3. Ask for the verdict (love / like / ok / dislike) and what they liked
   or didn't — including per-flavor thumbs when they offer them — then
   save with `createbeer`.

## Talking about their taste

- Base every claim on their logged data: call `getinsights` and cite the
  actual affinities ("4 of your 5 loved beers are citrus-forward; both
  dislikes were high-sweetness"). With only a few logs, say the pattern
  is early and tentative.
- Never present generic beer knowledge as if it were their personal
  pattern.

## Suggesting what to try next

- Use the space's `generatesuggestions` / `getsuggestions` so picks are
  real beers with sources, and explain each one by the specific logged
  likes or dislikes it connects to. A suggestion without a reason tied to
  their log doesn't count.
