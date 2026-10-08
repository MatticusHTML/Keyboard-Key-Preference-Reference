# Switchboard

Last updated: October 8, 2026.

A single-page site replicating the Keychron Switch Tester 100 Max Edition's Super switch layout as a clickable grid. Coworker preferences appear on the grid. Click any switch to explore its feel, expected sound, spring resistance, and preferences.

Each popup includes visual guides for audible click, typing loudness, and tactile bump, plus a keypress illustration and Previous/Next buttons. An expandable beginner guide explains the switch types. The footer links to the original Amazon tester and the official Keychron specifications.

## Files

- `index.html` - the whole site. No build step, no dependencies beyond Google Fonts. Open it directly in a browser or deploy as-is.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Repo Settings > Pages > set source to the branch this file lives on (usually `main`), root folder.
3. GitHub will serve `index.html` automatically at `https://<username>.github.io/<repo-name>/`.

## Editing who likes what

Near the top of `index.html`, inside the `<script>` tag, are two arrays:

```js
const FRIENDS = ["Matticus","Katelyn","Dan","Cam","Kassidy","Vanessa"];

const LIKES = {
  // "7-2": ["Katelyn","Dan"],
};
```

`FRIENDS` is just a reference roster. `LIKES` is what actually shows up on the site: each key is a switch id (matches the small position tag in each key, like `7-2`), and the value is an array of names who like that switch. Add a new entry or add a name to an existing array, save, redeploy.

This is intentionally not editable from the live site itself, only by editing the source.

## Data model

Each entry in the `SWITCHES` array looks like:

```js
{id:"7-2", n:"Box White", t:"C", w:"l", f:"klBox", yours:1}
```

- `t` - type: `L` linear, `T` tactile, `C` clicky, `M` magnetic
- `w` - approximate spring weight: `l` light, `m` medium, `h` heavy; `a` indicates adjustable actuation on magnetic switches, not an adjustable spring
- `feel` - optional physical feel for a magnetic switch (`T` tactile); magnetic switches otherwise use linear feel here
- `f` - family key, looks up its description in `DESCRIPTIONS` and its brand in `BRAND_OF`
- `yours` - optional flag, marks Matticus's own switch (Kailh Box White)
- `u` - optional flag, marks switches with unconfirmed specs (newer or boutique releases)

## Notes on accuracy

Manufacturer references are linked inside each popup through `PROFILE_SOURCES`. The sound and bump bars are qualitative expectations based on the mechanism and damping, not recordings, decibel measurements, or measured force curves. Keycaps, the keyboard case, plate, desk, and typing force all change the actual sound. Spring weight labels are approximate.

Entries flagged with `u:1` have provisional specifications and show dashed, unconfirmed bars. `getProfile()` handles linear/tactile magnetic feel, silent designs, and the stronger click of Box Jade/Navy. Keep unknown variants unconfirmed until there is a reliable source or firsthand tester feedback.

Magnetic keyboards can adjust the registration depth in software. That does not change their physical spring weight or tactile bump, and the passive tester has no electronics to demonstrate software features.
