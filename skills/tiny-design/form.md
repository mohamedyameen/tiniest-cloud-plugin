# Designing a form — sign-ups, surveys, bookings, requests

> If the person has design standards of their own — a design system, components, a brand guide, an app or site to match — follow those, and use this playbook only for what they leave open. If they gave none, follow it all.

People fill it in once, often on a phone, often in a hurry. Every field is a cost to them:
ask only for what you will use.

## Shape

- One column, in the order people think about the answers; related fields grouped under a
  short heading (`fieldset` and `legend`).
- Labels above the field, always visible — never a placeholder standing in for the label; a
  hint under the label when the answer needs an example; mark the optional fields instead of
  every required one.
- A placeholder in every field as well: a friendly, contextual prompt or example answer for
  this form (a question the field answers, or a sample answer in the expected format), never
  the label repeated or "Type here…".
- The right control: radio buttons for up to five choices, a select or searchable list for
  more, a segmented control for two or three, checkboxes for several; the app's calendar in a
  popover for dates (never the browser's date input), with the time zone said when it matters.
- The right keyboard and autofill: `type` (email, tel, url, number), `inputmode`, `autocomplete`
  and a meaningful `name`; paste never blocked.
- Long forms become steps with a progress indicator and a review step before sending; a draft
  kept in `tiny.db` means nobody loses what they typed.

## Behaviour

- Validate when a field is left, not on every keystroke; the message sits under the field,
  says how to fix it, and is linked to it (`aria-describedby`) and announced.
- The submit button stays enabled until sending starts, then shows progress; on a failed
  submit, focus moves to the first problem.
- The submit button is never a scroll away. On a form taller than the screen it sits in a bar
  pinned to the bottom (`sticky bottom-0`, or just above the bottom navigation in an app, with a
  solid background, a border on top and the phone's safe area below) with a one-line summary of what is being sent ("‹what› · ‹when›", "‹count› items ·
  ‹total›").
- Success is a real moment: say it worked and what happens next (a confirmation, the next
  step, when they will hear back) — not a form that silently empties.
- A visitor without an account can submit only where the owner allows it (open submissions);
  give the prefix a schema in the rules file and consider the built-in spam check, as the
  guide describes. Whoever runs it sees the replies in the app, in the dashboard's Data screen,
  or exported as a spreadsheet — and can get a notification for each (`tiny.notify` or a job).

## Checks

- It can be completed on a phone with one thumb, with the keyboard never covering the field.
- Every error can be understood without seeing colour.
- Nothing is asked twice, and nothing is asked that is not used.
- Then the general checklist, "Before you call it done".
