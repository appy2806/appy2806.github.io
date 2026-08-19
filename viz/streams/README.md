# Stellar streams viewer — embedding

The page at `viz/streams/index.html` ships with the defaults used on
[arpitarora.space](https://arpitarora.space/): a side-by-side evolving/static
comparison, 100 streams, auto-rotating. Every default can be overridden with a URL
query parameter, so another site can pin the view it wants without a code change.

## Presets

A preset is one short, stable URL to hand to a third party. Individual parameters
still override it, so it is a starting point rather than a lock.

| Preset | View |
| --- | --- |
| `?preset=press` | Single evolving pane, no overlay text, no eye button. Gear and fullscreen stay visible. Fullscreen is the same view at full size — still text-free — so the gear is how a reader explores; switching to a side-by-side view there brings back the pane labels. |

```html
<iframe style="border: 0; background: #000;" title="Stellar streams in evolving models"
        src="https://arpitarora.space/viz/streams/index.html?preset=press"
        width="100%" height="640" allowfullscreen="allowfullscreen"></iframe>
```

## Parameters

| Parameter | Values | Default | Effect |
| --- | --- | --- | --- |
| `model` | `evolving`, `static`, `both` | `both` | Which model fills the frame. `both` is the side-by-side comparison; the others are a single pane. |
| `streams` | `1`–`200` | `100` | Number of streams drawn. |
| `size` | `0.05`–`0.5` | `0.25` | Point size. |
| `disk` | `0`–`2` | `1` | Milky Way disk brightness. |
| `rotate` | `1`, `0` | `1` | Auto-rotate on load. |
| `speed` | `0.05`–`2` | `0.25` | Auto-rotate speed. |
| `text` | `1`, `0` | `1` | Title, source line, interaction hint, viewport labels, and credits. |
| `gear` | `1`, `0` | `1` (`0` with `embed=1`) | The controls gear. |
| `eye` | `1`, `0` | `1` (`0` when `text=0`) | The hide-text (eye) button. It has nothing to toggle without overlay text, so it follows `text` unless set explicitly. |
| `labels` | `on`, `off`, `side` | follows `text` | The per-pane model names. `side` shows them only in a side-by-side view, where they are the only way to tell the two models apart. |
| `fs` | `1`, `0` | `1` | The fullscreen button. |
| `fsmodel` | `evolving`, `static`, `both`, `keep` | `keep` | View to switch to when entering fullscreen. Exiting restores the previous view. |
| `fschrome` | `1`, `0` | `1` | Whether fullscreen restores the chrome this embed hid. `0` keeps the embed's own look at full size, leaving the gear as the way to explore. |
| `embed` | `1`, `0` | `0` | Shorthand for the site's own iframe: hides the gear, keeps the eye and fullscreen. |

Booleans also accept `true`/`false`, `yes`/`no`, `on`/`off`. An unparseable value falls
back to the default, so a typo in someone else's iframe degrades to the standard view.

Two things hold regardless of the parameters:

- The gear panel is always wired, even where it is hidden, so any embed can be promoted
  to the full experience without reloading.
- Sliders open on the values that embed was given, and each reset button returns to
  them — an embed's own settings are the defaults for its readers.

One thing to watch: `text=0` hides the credits footer, and with `fschrome=0` it stays
hidden in fullscreen too, so such an embed carries no on-canvas attribution. Add
`&text=1`, or rely on the host page's own caption, where credit needs to be visible.

## Examples

```
index.html?embed=1                       the arpitarora.space iframe
index.html?preset=press                  press embed
index.html?preset=press&fschrome=1       press embed, but fullscreen restores the full site chrome
index.html?preset=press&fsmodel=both     press embed, fullscreen opens the comparison
index.html?model=evolving&text=0&gear=0&eye=0&fs=0&streams=40
                                         bare single-pane loop for a slide
```
