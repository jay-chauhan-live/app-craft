---
name: app-craft
description: Design and behaviour principles for building apps that feel like real native apps, on any stack (native Android, native iOS, Flutter, React Native, Capacitor/Ionic, PWA, responsive web). Use when designing, building, reviewing or auditing app screens and flows - navigation and Back, tabs and swipe, offline-first and sync, loading skeletons, touch feedback, sheets and forms, versioning and update screens, security of tokens and sign-in, empty/error states, and the audit method. Triggers on "native feel", "offline", "skeleton", "back button", "swipe between tabs", "bottom navigation", "mobile UX", "premium app UI", "app audit".
---

# app-craft

How to build an app so it behaves like a real native app and looks premium, whatever the stack. These principles come from building and repeatedly correcting a real phone-first admin app; every rule exists because its absence was a bug someone noticed.

The rules are platform-neutral. Each reference file states the principle first, then how to do it on each stack (see `references/platforms.md`). When a rule conflicts with the platform's own convention on the device in your hand, the platform convention wins.

## The ten laws

1. **Familiar beats clever (Jakob's Law).** Use the patterns people already know from the best apps on their device: bottom tab bar (max 5), large title that collapses, inset grouped lists, bottom sheets, swipe actions, pull to refresh. Never invent navigation.
2. **One way to move between sections: no page-selection chips.** Do not put a row of pills/chips/tabs at the top to pick "which page". Sections are tabs, sub-pages are rows that push a screen, filters are a control inside the screen. See `navigation.md`.
3. **Back always means "up", never "whatever came before".** Same result from the app's Back arrow and the system Back button. Close what is open on top first, then go to the screen's parent, then to Home; leave the app only from Home. See `navigation.md`.
4. **Swipe is physical.** If the app supports swiping between tabs, the screen follows the finger and the neighbour slides in beside it. Navigating after the gesture ends (a "click") is not a swipe. See `navigation.md`.
5. **Offline first, honest second.** Every screen already opened loads instantly from a saved copy with or without a network; writes made offline are queued and sent once, exactly once; only things that truly need the server say "You're offline". See `offline-first.md`.
6. **Skeletons are the real screen without data.** Same structure and size per screen, never one generic placeholder. See `loading-states.md`.
7. **Respond before the server does.** Pressed state in under 100 ms, optimistic updates with rollback, loading state on every button, nothing silent. See `native-feel.md`.
8. **Phone first, then every size.** Design at 320-390 px, then widen. No horizontal page scroll, nothing outside the screen (add buttons, FABs), safe areas respected, text never breaks mid-word, nothing truncates the thing the user came for. See `ui-design.md`.
9. **Say what a thing is.** No unlabeled numbers, badges or counts. A badge says what it counts and disappears once the thing is seen. Real names, not internal terms. See `ui-design.md`.
10. **Security and truth are defaults.** Secrets sealed and never returned to clients, sensitive changes need a fresh second factor, no invented content or data, and say plainly what was and was not verified. See `security-and-honesty.md`.

## How to work with this skill

- **Building a screen:** read `ui-design.md`, `loading-states.md` and `native-feel.md`; build the skeleton and the empty and error states with the screen, not later.
- **Adding navigation or a new section:** read `navigation.md`; update the parent map (Back) and the tab/swipe list in the same change.
- **Adding data or a write:** read `offline-first.md`; decide read-cached or queued-write or needs-connection, and make writes idempotent.
- **Shipping:** read `release-and-system.md` (version shown in the app and in the deploy message; an in-app System page with Check for updates).
- **Reviewing or auditing an app:** follow `audit-method.md`, which turns all of this into a checklist and a proof method (screenshots and measured numbers, not opinions).

## Never

- Never ship a generic spinner/skeleton for a screen that has a known shape.
- Never let Back depend on history you cannot see (a chat you closed must not come back).
- Never show a number without saying what it is.
- Never put page-selection chips at the top of a screen.
- Never leave an action button where it can scroll or sit off-screen on a small phone.
- Never say "done" without having run it and looked at the result.
