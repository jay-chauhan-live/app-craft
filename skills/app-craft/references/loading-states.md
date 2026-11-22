# Loading, empty and error states

## Skeletons
- A skeleton is the real screen drawn without data. Build one **per screen type** using the same components and classes as the real screen so heights and positions match at phone and desktop widths. A generic "header plus list" skeleton for every screen is a bug: System, settings lists, forms, tables, detail pages, dashboards and chat lists all look different.
- Required families: dashboard/home, grouped settings list, list with avatars (chats/contacts), table, stat cards plus chart, form, detail, profile, system/about.
- Skeleton appears the instant a link is tapped (do not wait for the server) unless the screen opens faster than about 90 ms. When the real screen arrives it replaces the skeleton without a second animation.
- A skeleton for a destination screen must also be usable as the "neighbour" while swiping tabs.
- **Prove it:** measure skeleton height versus real screen height for each screen type at 390 and 1280 px; they should be within about 10%, and nothing may jump when data arrives.
- Respect reduced motion (static shade instead of shimmer). Announce loading once to screen readers, hide the bars.
- Screen-level "Loading…" text or a spinner in the middle of an empty page is not acceptable; small inline spinners (a button, a refresh) are fine.

## Empty, error and offline
- Empty: say what belongs here and the one action to fill it. Never a blank page.
- Error: plain words, what failed, what the user can do, a Retry that works. Keep the user's input.
- Offline: see offline-first; show saved content with the indicator, and the message only where the server is truly needed.
- Partial: show what you have; do not block a whole screen on one failed card.
