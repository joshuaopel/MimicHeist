# Mimic Heist

A browser stealth game where you play a living Mimic taking treasure back from invading heroes. Disguise yourself as dungeon furniture, dodge vision cones, lure heroes with fake loot, and slip out the portal.

**Play it:** open `index.html` via any static server, or enable GitHub Pages on this repo (Settings → Pages → deploy from `main`).

> Note: opening `index.html` directly from disk (`file://`) blocks `fetch`, so the game falls back to its built-in campaign. Use a local server to test repo levels: `python -m http.server` then visit `http://localhost:8000`.

## Controls

| Key | Action |
|---|---|
| WASD | Move |
| Shift | Sneak (quieter, slower) |
| E | Copy nearby object / revert to Mimic |
| Space | Grab treasure |
| Q | Drop fake treasure (lure) |
| R | Chest Snap (scare nearby heroes) |
| M | Toggle minimap |
| Esc / P | Pause |

Touch controls appear automatically on mobile.

## Level flow

`levels/manifest.json` defines the campaign — **the order of the `levels` array is the play order**:

```json
{
  "name": "Mimic Heist Campaign",
  "levels": [
    "the_pantry.json",
    "the_treasury_depths.json",
    "the_grand_vault.json"
  ],
  "unlockAll": false
}
```

- `unlockAll: false` → levels unlock sequentially as you beat them
- `unlockAll: true` → everything playable immediately
- If the manifest is missing or unreachable, the game uses its built-in campaign

## Adding a level

1. Build it in **Mimic Forge** (the level editor) and fill in name, author, and description
2. Export — you get a `.json` file (custom art is embedded in the file)
3. Drop the file into `levels/`
4. Add its filename to the `levels` array in `manifest.json` wherever it belongs in the flow

Players can also drag any level `.json` onto the game window to play it without touching the repo.

## Level format

Levels are plain JSON: tile grid (`0` void, `1` floor, `2` wall, 64px tiles), spawn, portal, goal, props (disguise sources), treasures, heroes with patrol waypoints, torches, optional `art` slots (data-URL PNGs), plus `name`, `author`, `blurb`.
