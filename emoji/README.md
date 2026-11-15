# OpenMoji engraving masks

These local assets contain all **3,944 standard fully-qualified Unicode 17.0
emoji** from OpenMoji **17.0.0**. They include joined sequences, skin-tone
combinations, country flags and subdivision flags. OpenMoji-specific extras and
standalone emoji components are excluded. Apple-specific drawing files are not
included.

The artwork is adapted from [OpenMoji](https://openmoji.org/), by the OpenMoji
contributors at HfG Schwäbisch Gmünd and other contributors. It is distributed
under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). The complete
license is in `LICENSE.txt`. Unicode data is distributed with its accompanying
`LICENSE-UNICODE.txt`. Pinned source URLs and SHA-256 hashes are recorded in
`attribution.json` and in the importer.

## Rendering and changes

The `openmoji-00.json` through `openmoji-30.json` files are requested on demand.
Each maps the original OpenMoji hexadecimal code to:

```json
{
  "viewBox": "0 0 72 72",
  "markup": "<g>...allowlisted SVG geometry...</g>",
  "rendering": "mask"
}
```

Render this markup in a luminance mask with a black background. White reveals
aluminum; black is unengraved background. Ordinary emoji use authored line art
without tracing color/shading regions. Grinning mouths omit teeth dividers;
the skull omits tooth bars and has a closed jaw; sunglasses omit tiny duplicate
bridge/rim details; fire uses one closed flame silhouette. Flags and artwork
without line art retain outlined color-region boundaries with black knockouts.
Skin-shadow layers are omitted. Original filled thin line contours remain thin
filled mask contours, which avoids double outlines. All paints are black or white,
and no image, font, script, external reference, CSS, or SVG ID is accepted.

The complete **color** SVG source is intentionally used. OpenMoji's black SVG
set omits some color-defined boundaries: for example, its black US flag contains
only the outer rectangle. The adapted masks retain the internal flag details
where they are needed to identify flags or artwork without line art.

`src/data/emoji-catalog.json` contains searchable names, keywords, categories,
canonical Unicode presentation strings and the chunk for each code. Mixed-tone
sequences use the first modifier for their palette tone filter; the complete
sequence remains intact. The browser only loads the chosen geometry chunk, so
the complete mask library is not included in the initial application script.
`src/data/emoji-index.json` is the compact validation/index subset, with tuples
of `[emoji, code, name, chunk]`; the full searchable catalog can load separately.

## Rebuilding

From `emblem-studio`:

```sh
python scripts/import-openmoji.py
```

The importer uses Python's standard library and verifies every pinned source
checksum. Downloads are cached in the operating-system temporary directory as
`bespoke-openmoji-17.0.0`. It verifies exact coverage against Unicode 17.0's
fully-qualified emoji test data, validates the 72 × 72 coordinate system, and
rejects unexpected SVG elements or external references rather than silently
dropping geometry.
