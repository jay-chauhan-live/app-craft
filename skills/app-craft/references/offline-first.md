# Offline first

Goal: the app opens and works like a native app with no signal, and syncs by itself when the signal returns.

## Three kinds of operation
1. **Reads** (lists, summaries, details): keep the last good answer on the device, keyed by request. Show it immediately, refresh in the background, replace when the network answers. Offline: show the saved copy.
2. **Queued writes** (create an entry the user does often, such as a transaction, a note, a message draft): save to a local outbox, show it in the list immediately marked "Waiting to sync", send when online.
3. **Needs the server** (payments, sign-in, anything that must be confirmed, first-ever open of a screen): show a clear message "You're offline. This needs a connection." and keep the user's input.

Decide which kind each feature is when you build it.

## App shell and screens
- Cache the app's static assets forever (hashed files) and the screens the user has opened (stale-while-revalidate for basic screens such as contacts, messages, calls, settings; network-first with a short timeout, about 3 s, for the rest).
- A screen opened once must open offline in about a second. A screen never opened gives the offline message, not a browser error page.
- Never cache API calls in the generic cache; use the saved-reads store above so you control keys and size (bound it, for example 400 entries).
- A small unobtrusive indicator says "You're offline" and "N waiting to sync" / "Syncing…".

## Outbox and sync
- Every queued write has a unique client-generated id sent to the server as an idempotency key (for example `sourceRef: app:<uuid>`); the server dedupes on it, so a retry after a dropped response can never create a duplicate.
- Send oldest first. Stop at the first connection failure and retry later (on regain-connectivity event, app foreground, and a timer). A server refusal (validation) keeps the item with its error visible so it can be fixed; it never blocks silently.
- Single-flight: only one sync runs at a time.
- When something was sent, tell open screens (event or notifier) so they reload, and refresh server-rendered data.
- Edits and deletes of items that exist only on the server, and anything not designed for queueing, need the connection. Do not half-queue them.

## Hygiene
- Saved data can be sensitive (money, messages). **Wipe everything at sign-out**: local database, caches, outbox.
- Store versions: when the stored shape changes, bump the store version and migrate or drop.
- After a new deploy, cached screens must not trap the user on an old version: version the caches, check for an update on open, and offer "Reload" without losing typed input.
- Service workers/background sync exist on web and Capacitor; native iOS/Android use a local database (Core Data/SwiftData/Room), a persisted queue and WorkManager/BGTaskScheduler; Flutter/React Native use SQLite/MMKV plus the same outbox pattern. The three-kinds model and idempotency key are the same everywhere.
