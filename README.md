# Password Strength Analyzer

A single-file, dependency-free password strength analyzer that runs entirely in the browser. No backend, no network requests, no tracking — the password never leaves the page.

## Features

- **Rule checklist** — length (12+ characters), uppercase letter, number, special character, and dictionary-word detection, each shown as a live pass/fail item.
- **Entropy estimate** — calculated from character-pool size and password length, with penalties applied for weak structure (dictionary words, sequential runs, keyboard walks, repeated characters). A short note explains what the number means.
- **Dictionary detection with leetspeak normalization** — common substitutions (`@`→a, `0`→o, `1`→l, `3`→e, `5`→s, `7`→t, etc.) are normalized before the dictionary scan, so passwords like `P@ssw0rd!` are still flagged.
- **Pattern detection** — sequential runs (`abc`, `321`), keyboard walks (`qwe`, `asd`), and repeated characters (`aaa`).
- **Strong password generator** — one click fills the field with a 16-character password guaranteeing all four character classes.
- **Copy to clipboard** — copies the current field value with a brief confirmation.
- **Show/hide toggle** for the password field.

## Why it's local-only

Everything — the dictionary list, the entropy math, the pattern checks — runs client-side in plain JavaScript. There's no server component and nothing is persisted or transmitted, so it's safe to use with real passwords while testing.

## Getting started

This is a single static HTML file with no build step and no dependencies.

## How the scoring works

- **Entropy** is estimated as `length × log2(pool size)`, where pool size grows with the character classes present (lowercase, uppercase, digits, symbols).
- That raw entropy is then discounted when the password contains a dictionary word (after leetspeak normalization), a sequential run, a keyboard-adjacent pattern, or 3+ repeated characters in a row — since these make a password far more guessable than raw entropy alone suggests.
- The overall strength meter combines this adjusted entropy with the basic rule checklist.

## Limitations

- The built-in dictionary is a small demo-scale list (~50 common passwords/words), not a full breach-corpus list. For production use, swap in a larger word list (e.g. the top 10k–100k most common passwords).
- Entropy is an estimate, not a guarantee — it's meant to guide better password choices, not to certify a password as "uncrackable."


