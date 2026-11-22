# Security and honesty

## Secrets and sign-in
- Tokens and credentials stored by the app are encrypted at rest (authenticated encryption, key outside the database), opened server-side only at the moment of use, never returned to any client page, never logged.
- Adding, replacing or removing a credential, and other sensitive account changes, need a **step-up**: a fresh second-factor check just before.
- Prefer passkeys plus a second factor. Browser sessions expire (for example 30 days); a trusted native app session may slide.
- Least privilege: request only the scopes needed (for example read-only access to contribution data).
- Sign-out wipes local data (see offline-first). Local data on a device is treated as sensitive.

## Data
- Idempotency keys on every retried write. Server validation is the truth; the client only helps.
- Audit log for sensitive actions. Backups before migrations.

## Honest reporting
- Say what you ran and what you saw. If something was not tested (a real phone, a real device, a native build), say that plainly instead of implying it works.
- Never invent content, numbers, ranking promises or biography. Label sample data.
- If a requested change is risky or outward-facing (publishing, sending, deleting), confirm first unless the owner already authorised exactly that.
