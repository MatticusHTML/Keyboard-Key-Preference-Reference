# Project context

Switchboard is a single-file static HTML site for browsing 100 mechanical keyboard switches (the lineup from a Keychron 100 Max Edition switch tester). It's a personal project for Matticus and his friend group, to be hosted on GitHub Pages.

## Constraints, keep these

- Single self-contained file. No build step, no framework, no bundler. Plain HTML/CSS/JS in `index.html`. This matches the owner's other GitHub Pages projects, keep it that way unless explicitly asked to change the architecture.
- No `localStorage` or `sessionStorage`. No backend. The `LIKES` data object is static and hand-edited, never live-writable from the page itself. This is deliberate, not a missing feature, the owner wants the site itself to only be changeable by him, not by visitors.
- Never use em dashes or en dashes anywhere in generated content (titles, copy, code comments, commit messages). Use a plain hyphen (`-`) instead. This is a standing preference, apply it to everything written for this project and this owner going forward.

## Data model (inside the `<script>` tag in index.html)

- `SWITCHES` - array of 100 objects: `{id, n (name), t (type: L/T/C/M), w (weight: l/m/h/a), f (family key), yours?, u?}`
- `DESCRIPTIONS` - dict keyed by family (`f`), one or two sentence feel description
- `COMPANIES` - dict keyed by brand (`keychron`/`gateron`/`kailh`/`huano`), which companies use that brand's switches
- `BRAND_OF` - maps a family key's two-letter prefix (`ky`/`ga`/`hu`/`kl`) to its brand
- `FRIENDS` - reference roster array, not functionally required by the UI
- `LIKES` - object mapping switch `id` to an array of friend names. Empty by default. This is the only part of the data meant to be edited over time.

`yours:1` marks Matticus's own switch (Kailh Box White, id `7-2`). `u:1` marks switches with unconfirmed public specs, newer or boutique Kailh releases mostly, these get a disclaimer line in the popup instead of a confident-sounding description.

## Design tokens

- Fonts: Space Grotesk (headings), Inter (body), JetBrains Mono (position tags, technical labels)
- Type colors: linear blue, tactile amber, clicky red/coral, magnetic violet, defined as CSS custom properties with light and dark mode variants via `prefers-color-scheme`
- Grid cells are styled to resemble physical keycaps (colored top edge by type, lift on hover, press animation on click)

## Common follow-up requests to expect

- Adding a new friend's name to `LIKES` for a given switch id
- Adding a new friend to `FRIENDS`
- Correcting a switch's type/weight/description if the owner tests it and finds the guess was wrong, especially for anything flagged `u:1`
- Possibly splitting into separate files (styles.css, script.js) if the project grows, but default to keeping it a single file unless asked
