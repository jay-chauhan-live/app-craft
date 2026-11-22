# Navigation, Back and swipe

## Structure
- **At most five bottom tabs** for the daily-use sections (example: Home, Chats, Inbox, Money, Forecast). Everything else lives under a profile/avatar menu ("More", Settings, Admin) at the top right, not in a sixth tab.
- **Group related things in a hub screen** instead of many tabs. Example: Inbox groups chats, messages, calls, mail, webhooks and leads as grouped rows with counts, and opens each as its own pushed screen.
- **Sub-pages are rows** (chevron) that push a screen. Filters, view modes and sort are controls inside the screen (segmented control, menu, sheet) and change content in place.
- **No chip/pill/tab strip for choosing pages.** If something looks like "tabs across the top that switch pages", turn the pages into rows of a hub or a segmented control inside one page. A segmented control that switches views of the SAME data (day/week/month) is fine; one that switches between different pages is not.
- User-orderable pills (for example filters inside a chat list) may be reordered by the user; the order is saved per user and the first one opens by default.

## Back means up
Define a **parent map**: for every screen, the screen above it. Home has no parent. Rules, in order, identical for the app's Back arrow, the system Back button and the Back gesture:
1. If something is open on top of the screen (dialog, sheet, a chat opened from a list, a detail pane, a search overlay), close it. One step.
2. Otherwise go to the screen's parent: a page to its hub or tab, a hub to Home, a main tab to Home.
3. At Home, Back leaves the app (or does nothing on iOS).
Navigate to the parent by **replacing** the current history entry, so the screens in between are never revisited.
- Example that must hold: open a chat, close it with the app's arrow, press the system Back: you land on Home, not on the chat.
- Opening something from a notification or deep link must still have a sensible parent (the list), not itself.
- Anything that opens "on top" registers a **layer** that owns exactly one history/back-stack entry; closing it any way (its own button, Escape, swipe down) removes that entry.
- Keep the parent map in one file and add every new screen to it in the same change.

## Swipe between tabs
- Only on a tab root screen. Never from the screen edge (it belongs to the system Back gesture; keep ~28 px away), never inside text fields, dialogs, an open chat/composer, horizontally scrollable carousels that can still scroll that way, or rows with their own swipe action.
- **The screen follows the finger** (translate with the touch), the neighbouring tab slides in beside it (a skeleton of it is acceptable while it loads), release settles at about one third of the width or on a quick flick, otherwise springs back. Past the first/last tab it stretches slightly and returns.
- Left-to-right moves to the tab on the left; right-to-left to the tab on the right. Do not reverse.
- Decide direction while the finger moves, not on release (platforms cancel touches once a scroll starts). Lock to horizontal after about 10 px when clearly more horizontal than vertical.
- Prefetch the neighbouring tabs so landing is instant; skip the usual screen transition after a swipe (the slide was the animation).
- Tapping the active tab scrolls to top, again resets that tab's stack.
