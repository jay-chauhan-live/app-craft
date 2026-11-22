# Audit method

Use this to find what is not native-feeling or not premium, and to prove the fix.

## Setup
- Run a production build against a **copy** of the data (never the live database), with sample or copied data, a signed-in session, and scheduled jobs off.
- Use a touch-emulated browser at 320, 360, 390 and 1280 px, dark and light, and the real device when possible.

## Pass 1: screens (one reviewer per area works well; parallel reviewers are fine)
For every screen: screenshot at the widths above and look at it. Check: overflow, clipped/off-screen buttons, mid-word wraps, unlabeled numbers, chip bars, contrast, safe areas, empty and error states, long content, 0 and 1000 items.

## Pass 2: behaviour
- Navigation: Back from every screen (app arrow and system), from a notification, after closing a chat; swipe between tabs in both directions and the guard cases (edge, vertical, carousel, row, input).
- Offline: warm the screens, go offline, reload each basic screen (time it), create a queued write, reconnect, verify exactly one copy on the server and an empty outbox; sign out and verify local data is gone.
- Loading: for each screen type compare skeleton and real height; slow the network and watch for jumps.
- Touch/feel: pressed states, selection, overscroll, keyboard, sheets (drag, backdrop, Back), optimistic actions with a forced failure.
- Performance: CPU throttled, time tap to first visual change for the five commonest taps.

## Pass 3: report
A table: item, found, fixed, not fixed, evidence (screenshot or number). Separate list: needs a new native build. State what was not tested.

## Fix style
- Prefer one global fix (token, shared component, shell hook) over per-screen patches.
- Add the regression check (a script that fails when the rule breaks) next to the fix when the rule can be tested.
