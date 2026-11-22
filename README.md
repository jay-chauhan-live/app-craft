# app-craft

Design and behaviour principles for building apps that feel like real native apps, on any stack: native Android, native iOS, Flutter, React Native, Capacitor/Ionic, PWA or responsive web.

It is a skill in the `SKILL.md` format used by coding agents, and it is also plain, readable guidance for people.

## What is inside

| File | Covers |
| --- | --- |
| `skills/app-craft/SKILL.md` | The ten laws and when to read what |
| `references/navigation.md` | Tabs, no page-selection chips, Back means up, a swipe that follows the finger |
| `references/offline-first.md` | Saved reads, a queued outbox, idempotent sync, honest offline messages |
| `references/loading-states.md` | Per-screen skeletons, empty, error and offline states |
| `references/native-feel.md` | Touch, selection, scrolling, safe areas, sheets, haptics, tap-to-response |
| `references/ui-design.md` | Visual language, layout rules, labelled numbers, content discipline |
| `references/release-and-system.md` | Visible versions, the System screen, deploy hygiene |
| `references/security-and-honesty.md` | Sealed secrets, step-up checks, honest reporting |
| `references/audit-method.md` | How to audit and prove a fix |
| `references/platforms.md` | The same rules mapped to each stack |

## Install

Copy the skill folder into your skills directory:

```bash
mkdir -p ~/.claude/skills
cp -r skills/app-craft ~/.claude/skills/
```

## Licence

MIT
