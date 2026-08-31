# Inbox Zero — waitlist landing

Single-screen landing, built as a measured reconstruction of the source mockup: chrome headline with
bitmap characters spliced in, satin-metal envelope with a glowing "0" badge, and a waitlist bar.

- `index.html` — everything inside it (CSS + inline SVG + the form script). No build, no dependencies.
- Fonts: Space Grotesk, Pixelify Sans, Space Mono (Google Fonts).
- Everything scales off `--k` = 1% of a 1993px reference width, locked above that width.

**Live:** https://daniel-figutech.github.io/inbox-zero-landing/

## The materials are measured, not eyeballed

The mockup was sampled pixel by pixel and each material reproduces specific numbers:

| | reference | this build |
|---|---|---|
| headline horizontal sheen amplitude (10 column buckets) | 80 / 82 / 74 | 77 / 76 / 69 |
| headline core pixel mean, per line | 158 / 148 / 158 | 162 / 153 / 162 |
| per-glyph bevel (x-height glyph top ≥ tall glyph top) | pass | pass |
| envelope brightness ridge | (70% w, 2% h) → (2% w, 67% h) | same axis |
| envelope top-left / top-right luminance | 81 / 168 | 85 / 165 |
| badge black-face mean (the aura) | 29.9 | 43.1 |
| badge black-face p90 | 36.0 | 83.0 |
| composition, envelope top / page height | 56.98% | 56.98% |

Three things drive the look and are easy to break:

1. **The headline is two blended background layers**, not one gradient — a per-glyph bevel
   (`--bevel`, blended `hard-light`) over a per-line horizontal sheen (`.l1/.l2/.l3`). The bevel
   carries two bright stops, one at the cap line and one at the x-height line, which is what gives
   short letters their own top rim. `background-blend-mode` does apply before
   `-webkit-background-clip:text`; if a browser ever drops it, the page degrades to the vertical
   bevel alone, which still reads as chrome.
2. **The envelope gradient runs along the perpendicular of its brightness ridge**, vector (240, 506)
   in viewBox units. Rotating it flattens the metal instantly.
3. **The badge aura** is stacked blurred copies of the "0" clipped to the face, plus one wide copy
   that escapes past the bezel. The counter of the "0" is painted back to face tone afterwards —
   without that the bloom floods the hole and the ring stops reading as a ring.

## Wiring up the signups

The form posts to FormSubmit over AJAX and never leaves the page. Set `FORMSUBMIT_TARGET` near the
top of the script — it is the only line to touch. Read the comment above it first: **this repo is
public**, so prefer FormSubmit's random alias over your real address.

States handled: invalid address (shake), in flight (locked, "Sending…"), success (form spent),
network failure (message, auto-clears). Honeypot field included; no account or API key needed.
