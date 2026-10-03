# screesaver — Mac lockscreen animation collection

A fullscreen, animated **lockscreen experience for Mac**, built as a
zero-dependency web page. Open `index.html` in a browser and go fullscreen —
the background fades in first, then the character slides in, then click (or
press any key) to unlock.

> Note: macOS doesn't allow replacing the real lock screen, so this is a
> fullscreen simulation — convincing enough to demo, record, or project.

## The sequence

1. **Background** fades in alone (1400ms ease-out, slow 1.08→1 settle) —
   one focal point at a time.
2. **Character** enters with the selected animation (~650ms in), while the
   background dims slightly to hand it the focus.
3. **Clock + date** fade up, then the unlock hint — staggered 40ms apart.
4. **Idle**: the character gently floats; moving the mouse adds lerped
   parallax between background and character.
5. **Unlock**: click / any key → character and chrome exit fast (ease-in,
   ≤300ms), background blurs and pushes in, mock desktop fades up.

## The collection — 4 animations

| # | Name | What it shows off |
|---|------|-------------------|
| 1 | **Drift In** | Anticipation pull-back, then a spring overshoot settle |
| 2 | **Rise** | Dips first (anticipation), lands with a subtle squash |
| 3 | **Materialize** | Blur-to-sharp focus pull, quiet staging |
| 4 | **Arc** | Curved entry path with rotation — arcs beat straight lines |

Switch with the pill bar at the bottom, or keys `1–4`. `R` replays,
`Esc` re-locks from the desktop.

## Motion principles

Built against the `12-principles-of-animation` skill
(`~/workspace/skills/12-principles-of-animation/SKILL.md`):

- **Easing** — entrances ease-out (never linear); exits ease-in.
- **Physics** — overshoot via spring-like bezier, squash kept to 0.95–1.05,
  stagger capped at 50ms, `:active` scale on every control.
- **Staging** — sequenced focal points, dimmed background behind the
  character, explicit z-index layers.
- **Timing** — user-initiated motion completes ≤300ms; entrances share one
  duration family.
- Disney mapping: anticipation (pull-back/dip), arcs, secondary action
  (float + parallax), exaggeration (overshoot), slow in/out.

`prefers-reduced-motion` is respected — everything jumps to its final state.

## Files

```
screesaver/
├── index.html          # stage, clock, variant bar, mock desktop
├── css/style.css       # all keyframes, easings, layers
├── js/app.js           # sequencing, clock, parallax, unlock/lock
└── assets/
    ├── background.png  # the classroom backdrop
    └── person.png      # the character (alpha cutout)
```

## Try it

```bash
# easiest: double-click index.html, then fullscreen the browser (⌃⌘F on Mac)
# or serve it:
python3 -m http.server 8000
# → http://localhost:8000
```
