# Applying the rules on each stack

The laws are the same; the mechanism differs.

| Concern | Native Android (Compose) | Native iOS (SwiftUI) | Flutter | React Native | Capacitor / Ionic | Web / PWA |
|---|---|---|---|---|---|---|
| Tabs + parent-map Back | Navigation-Compose with a bottom bar; `BackHandler` implements "close layer, else parent, else exit" | `TabView` + `NavigationStack`; swipe-back is system, popping to a parent via path reset | `go_router` shell routes; `PopScope` for layers | React Navigation tabs + stacks; `BackHandler` | Router + `App` plugin `backButton` listener | History API with layers; `replace` to parent |
| Swipe between tabs | `HorizontalPager` | `TabView` with `.tabViewStyle(.page)` (if tabs are pages) or custom drag | `PageView`/`TabBarView` | `react-native-pager-view` | Touch handlers following the finger (translate + neighbour) | Same touch handlers; non-passive `touchmove` after locking horizontal |
| Offline reads | Room + repository | SwiftData/Core Data | `drift`/`sqflite` + repository | SQLite/MMKV + React Query persist | IndexedDB + service worker | IndexedDB + service worker |
| Offline writes | Room outbox + WorkManager | persisted queue + `BGTaskScheduler` | outbox table + `workmanager` | outbox + background fetch | outbox in IndexedDB, sync on `online`/visibility | same |
| Idempotent sync | client UUID sent as key, server dedupes | same | same | same | same | same |
| Skeletons | per-screen placeholder composables (shimmer) | `.redacted(reason: .placeholder)` per screen | `shimmer` per screen widget | per-screen skeleton components | per-screen components | per-screen components |
| Sheets | `ModalBottomSheet` | `.sheet` with detents | `showModalBottomSheet` | `@gorhom/bottom-sheet` | custom sheet component | custom sheet component |
| Haptics | `HapticFeedback` | `UIImpactFeedbackGenerator`/`.sensoryFeedback` | `HapticFeedback` | `expo-haptics` | Capacitor Haptics plugin (needs a new build) | `navigator.vibrate` where present |
| Safe areas / keyboard | `WindowInsets` | safe area + keyboard layout guide | `SafeArea`, `viewInsets` | `react-native-safe-area-context` | CSS `env(safe-area-inset-*)`, keyboard plugin | same CSS, `visualViewport` |
| Secrets at rest | Keystore | Keychain | `flutter_secure_storage` | Keychain/Keystore wrappers | server-side sealing; no secrets in the WebView | server-side sealing |
| Version/update screen | Play in-app updates + own version row | App Store version check + own row | same per platform | same per platform | web version + native build version rows | version endpoint + reload |

Notes
- Wrappers (Capacitor, Cordova, WebView shells) run the web rules plus native bridges: handle the hardware Back button, status bar, push, safe areas and haptics through plugins; changes to native plugins or permissions need a new app build, screen changes do not.
- On every stack the platform's own gesture and component conventions win over these defaults when they differ.
