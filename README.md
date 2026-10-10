# Pomodoro Timer

A single-file productivity timer for the Pomodoro Technique. Work in focused 25-minute sessions, take short breaks, and earn a long break after four sessions.

No build step, no dependencies, no install. Open `pomodoro.html` in a browser.

## Features

- **Start / Pause / Resume** in one button, plus **Reset** for the current interval
- **Visual countdown**: a ring that drains as time passes, with large digital time
- **State changes**: the whole page changes color for each interval
  - Focus: red
  - Short break: teal
  - Long break: indigo
- **Session tracker**: four dots fill as you complete focus sessions
- **Sound alert**: a short three-beep chime when an interval ends
- **Tab title countdown**: see the remaining time without leaving your current tab
- **Light and dark mode**: follows your system setting
- **Accessible**: keyboard operable, visible focus outlines, and reduced-motion support

## Usage

1. Open `pomodoro.html` in any modern browser.
2. Press **Start** to begin a 25-minute focus session.
3. When the timer ends, the next interval is queued up. Press **Start** to begin it.
4. Use **Pause** to stop temporarily and **Reset** to restore the current interval to full length.
5. Switch intervals at any time with the tabs at the top (Focus, Short break, Long break). Switching stops the running timer.

## The cycle

| Step | Interval    | Length |
|------|-------------|--------|
| 1    | Focus       | 25 min |
| 2    | Short break | 5 min  |
| 3    | Focus       | 25 min |
| 4    | Short break | 5 min  |
| 5    | Focus.      | 25 min |
| 6    | Short break | 5 min  |
| 7    | Focus       | 25 min |
| 8    | Long break  | 15 min |

After the long break, the session dots clear and the cycle starts over.

## Customizing

Interval lengths are set in the `MODES` object near the top of the script:

```js
const MODES = {
  focus: { mins: 25, label: "Time to focus", name: "Focus" },
  short: { mins: 5,  label: "Short break",   name: "Break" },
  long:  { mins: 15, label: "Long break",    name: "Long break" }
};
```

Change `mins` to adjust a duration. The number of focus sessions before a long break is set in the `finish()` function (`done >= 4`).

Colors are CSS custom properties (`--bg`, `--ink`, `--accent`) defined per mode at the top of the stylesheet, with separate values for dark mode.

## How it works

- The timer stores an end timestamp and recalculates the time left on every tick, so it stays accurate even if the browser throttles background tabs.
- The ring is an SVG circle whose `stroke-dashoffset` is updated as time passes.
- The chime is generated with the Web Audio API, so there are no audio files to load. Browsers require a user gesture before playing sound, so the audio context is created when you press **Start**.

## Notes

- The page uses the Bricolage Grotesque font from Google Fonts and falls back to the system font if it can't load (for example, when offline).
- Timer state isn't saved. Refreshing the page resets everything.
- Background tabs may delay the on-screen update slightly, but the chime and the displayed time stay correct.

## Browser support

Any current version of Chrome, Edge, Firefox, or Safari.

## Side-note

I was sick while making this, so if there are bugs please inform me.