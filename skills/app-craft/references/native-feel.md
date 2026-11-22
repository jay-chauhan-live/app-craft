# Native feel

Aim: a user holding the phone cannot tell it from a platform app. Check every item on a real device or a faithful emulator, not only a desktop window.

## Touch
- Every tappable thing has an immediate pressed state (opacity or background, under 100 ms in, soft out). No tap delay (`touch-action: manipulation` on web), no grey tap-highlight flash, no sticky hover on touch (hover styles only where hover exists).
- Targets at least 44 pt / 48 dp with comfortable spacing. Destructive actions are never the easy accidental target; confirm with a sheet.
- Swipe actions on rows (delete, archive, mark unread) with a reveal and a threshold; haptic tick at the threshold where possible.

## Text and selection
- Chrome (navigation, buttons, rows, headers) is not selectable and shows no long-press callout. Real content (message text, amounts, ids, addresses) is selectable/copyable. Inputs behave normally.
- Font sizes in inputs at least 16 px on web so the platform never zooms. System font stack (San Francisco / Roboto), tabular numbers for amounts, no layout shift when fonts load.

## Scrolling
- Momentum scrolling; overscroll handled deliberately: the app's own pull-to-refresh works, there is no browser pull-to-refresh or white bounce behind the page; the background colour behind everything matches the theme.
- Scroll position is restored when returning to a tab or screen. Body scroll is locked behind sheets and dialogs.
- Large titles collapse into the bar title on scroll; the bar is translucent where the platform does that.

## Layout
- Respect safe areas (notch, home indicator, gesture bar) on the top bar, tab bar, sheets and floating buttons. Use dynamic viewport units, not static 100vh.
- The keyboard never covers the focused field or the composer; bars move above it.
- No horizontal page scroll at any width; fixed bars never overlap content (content has matching bottom padding).

## Sheets, menus, pickers
- On phones, menus, selects, date pickers and filters open as bottom sheets: drag handle, dimmed backdrop, spring-like slide, close by dragging down, tapping the backdrop and the system Back. One shared sheet component for the whole app.
- Avoid desktop popovers and the platform's tiny native dropdown for primary choices (account, category).

## Instant response
- Optimistic UI for the common actions (toggle, mark read, archive, delete, add): the UI changes now; on failure roll back with a toast.
- Every button that waits shows a loading state and ignores repeat taps. Nothing is silent.
- Light haptics for toggles, success and destructive confirmation (platform haptic API; vibration API on web where it exists).

## Chrome and system
- Status bar style and colour match the theme in light and dark. App icon, splash colour and name correct; installed web apps open standalone without browser UI.
- Notifications open the exact screen, with a sensible Back. Badges reflect real unseen counts and clear when seen.

## Performance feel
- Tap to first visual change under 100 ms for the five commonest taps (switch tab, open a chat, open a form, open a menu, open a detail), measured with CPU throttled. Anything longer gets a skeleton or optimistic result at once.
- Lists virtualise or paginate; images have sizes and fade in without jumping.
