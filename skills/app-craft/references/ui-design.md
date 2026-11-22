# UI design

## Visual language
- Restrained and premium: one accent colour, neutral surfaces with clear elevation steps, generous spacing on an 4/8 pt grid, one icon family, consistent corner radius. Dark and light both designed, not inverted.
- Inset grouped lists (rounded groups with hairline dividers) for settings and lists on phones; cards for dashboards; tables only where wide screens need them (they become grouped rows on phones).
- Large title per tab screen, compact bar title when scrolled. Text hierarchy by size and weight, not by colour alone. Contrast at least 4.5:1 for body text.
- Charts: few colours, direct labels, no decoration; tabular numbers; empty charts say so.

## Layout rules found by repeated audits
- Design at 320, 360, 390, 430 and 1280. Nothing may overflow horizontally; text wraps at word boundaries (never mid-word for titles); long values truncate with ellipsis only when the full value is available elsewhere.
- Primary actions stay reachable and on-screen: an "Add" button never sits beyond the right edge or under the tab bar; on small screens put it in the title row or a floating button above the bar.
- Forms: label above each field, correct keyboard type, inline validation, the primary button reachable above the keyboard, no placeholder-only labels. Wording says what happens ("Move money", not "Transfer form").
- Dialogs on phones are sheets; confirmation text names the item and the consequence.
- Keep related things together: a "Messages" screen title and its subtitle on separate lines, not wrapped together.

## Say what it is
- Every badge, count or number has a label: "1 unread in the inbox", "3 not processed", not a bare "1". Use the user's words ("Bank mails", "Leads"), not internal names ("webhooks", "jobs") unless the user is technical and the term is theirs.
- Counts are about things not yet seen; they go away when the user looks at them (for example the missed-calls count clears after viewing the calls screen).
- Dates and times: relative for recent ("26 min ago"), absolute otherwise, in the user's locale and time zone. In chats show one date pill at a time (the day currently scrolled past), as messaging apps do.
- Media in chats and lists: videos show a thumbnail with a play mark and duration, images show a blurred placeholder first.

## Content discipline
- No content in code: visible text and images come from the content system, only layout chrome is hard-coded.
- Never invent facts about people, clients, numbers, dates or quotes; sample data in screenshots is labelled as sample data.

## Customisation
- User-ordered items (pills, shortcuts) are saved per user and restored; the first is the default.
