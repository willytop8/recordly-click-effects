# Recordly Click Effects

Three visual effects for recorded clicks: ripple, pulse, and burst.

## Screenshots

![Ripple effect](./assets/screenshot-ripple.png)
![Pulse effect](./assets/screenshot-pulse.png)
![Burst effect](./assets/screenshot-burst.png)

## Install

### From the Recordly Marketplace

1. Open Recordly and go to **Extensions → Browse**.
2. Search for "Click Effects".
3. Click **Install**.

### Manual (development)

1. Open Recordly, go to **Extensions → Open Directory** to find your extensions folder.
2. Clone this repo into that directory:
   ```
   git clone https://github.com/williamjvest/recordly-click-effects.git
   ```
3. Restart Recordly. **Click Effects** should appear as active in the Extensions panel.

## Settings

Open **Settings → Cursor → Click Effects**. All settings update live.

| Setting | Type | Default | Range | Description |
|---|---|---|---|---|
| Enable | toggle | on | — | Show/hide click effects |
| Style | select | Ripple | Ripple / Pulse / Burst | Visual style of the click effect |
| Color | color | `#2563EB` | — | Effect color |
| Size | slider | 1.0 | 0.5–2.5 | Overall size multiplier |
| Duration (ms) | slider | 600 | 200–1500 | How long the effect animates |
| Line thickness | slider | 2 | 1–8 | Stroke width for effect lines |
| Distinct right-click style | toggle | on | — | Use dashed lines for right-clicks |

Size scales relative to the scene area rather than the canvas, so effects look consistent across different export resolutions and padding settings.

## Styles

**Ripple** — Two concentric rings that expand and fade. The inner ring leads; an outer ring follows with a slight delay.

**Pulse** — A soft halo that scales up and fades out. Simple and clean.

**Burst** — Eight radial lines extending from the click point, like a starburst.

When **Distinct right-click style** is on, right-clicks render with dashed lines instead of solid ones.

## Development

Clone and symlink into Recordly for local testing:

```bash
git clone https://github.com/williamjvest/recordly-click-effects.git
cd Recordly
# Find your extensions directory via Extensions → Open Directory
ln -s /path/to/recordly-click-effects /path/to/recordly-extensions/recordly-click-effects
```

No build step required — Recordly loads `index.js` directly.

## Known limitations

- The effects are purely visual. They do not produce audio (click sounds).
- Export quality depends on the canvas resolution set in Recordly's export settings. The effects use `sceneWidth * 0.04 * size` as the base radius and `videoLayout.maskRect` for scene-aware sizing; they will scale correctly but may appear slightly different at very low or very high export resolutions compared to the preview.
- No API gap prevents faithful reproduction of the PR #425 effects. All three effects (ripple, pulse, burst) use only public Recordly Extension API methods: `registerCursorEffect`, `registerSettingsPanel`, `getSetting`, `setSetting`, and `log`.

## License

AGPL-3.0 — see [LICENSE](./LICENSE).

## Credit

This extension began as [PR #425](https://github.com/webadderallorg/Recordly/pull/425) against the Recordly codebase and was repackaged as a standalone extension at the maintainer's suggestion.
