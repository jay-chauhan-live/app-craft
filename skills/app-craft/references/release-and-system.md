# Releases, versions and the System screen

## Versioning
- Every production release has a visible, unique version: `<line>.<build>`, for example `1.1.63`. The line (`1.1`) lives in a VERSION file and is bumped by a person when a feature ships (new feature = next minor, big change = next major). The build number is the CI run number, added automatically, so no release can ever repeat a version.
- The version is baked in at build time and exposed by a tiny public endpoint (`/version`, no data) used by the app to check for updates.
- It appears in three places: the System screen, the deploy message (chat/Slack) title and a Version field, and the build logs.
- Native shells (Android/iOS wrappers) keep their own version that changes only when native code, permissions, icon, name or splash change.

## System screen (under Admin/Settings)
Shows: app icon and "up to date / update available" headline, **Check for updates** button, then rows: Version, Released (build time), native app version and build, Channel, Last checked. When an update exists show the latest version and an **Update now** button that reloads into it; if the user is typing, wait and show a Reload bar instead of interrupting.
- A running app reloads itself after a deploy only when safe (nothing being typed).
- Explain in one sentence what updates by itself and what needs a new native app.

## Deploy hygiene
- Production changes only from the main branch through CI. Self-hosted runners for speed; a failed stage reports to the same chat thread.
- Database changes: migration files generated from the schema, a backup before migrating, never edit applied migrations.
- Cache purge after deploy so no stale page makes the client fall back to full reloads.
- One deploy message per run with a thread reply per stage and the version in the title.
