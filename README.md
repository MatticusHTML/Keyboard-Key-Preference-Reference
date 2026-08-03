# Switchboard

A single-page site replicating the 100-switch tester layout as a clickable grid. Click any switch to see its type, relative weight, what it feels like, what companies use it, and who in the friend group likes it.

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
- `w` - relative weight: `l` light, `m` medium, `h` heavy, `a` adjustable (magnetic switches only)
- `f` - family key, looks up its description in `DESCRIPTIONS` and its brand in `BRAND_OF`
- `yours` - optional flag, marks Matticus's own switch (Kailh Box White)
- `u` - optional flag, marks switches with unconfirmed specs (newer or boutique releases)

## Notes on accuracy

Type and relative weight are reasonably confident based on standard naming conventions in the mechanical keyboard hobby. About 11 of the 100 switches are newer or boutique releases without solid public documentation, those are flagged with `u:1` and show a note in the popup rather than presenting a guess as fact.
