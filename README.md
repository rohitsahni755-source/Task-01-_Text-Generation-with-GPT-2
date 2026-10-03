# Lumen Studio

A prompt-driven generative image studio. Write a description and the studio synthesises an
original artwork from it, or load an existing picture and rework it with real pixel-level
treatments. Everything runs locally in the browser — there is no server, no upload and no
account.

---

## What it does

**Prompt → image**

1. The user writes a prompt.
2. A keyword lexicon reads the prompt and resolves the structure, palette and tone from it.
3. The prompt and a seed are combined into a deterministic random stream.
4. The selected structure turns that stream into a value field across the canvas.
5. The field is stretched, colour-mapped, shaded, grained and vignetted.
6. The result is displayed at full size and can be downloaded as a PNG.

**Image → image**

1. The user loads a picture (or sends a render over from the Studio).
2. Luminance is measured for every pixel; dominant colours are clustered for palette work.
3. The chosen treatment rewrites the pixels.
4. The result is displayed and downloadable.

## Features

- Six synthesis structures: Nebula, Strata, Cellular, Flow Field, Terrain, Mosaic
- Fourteen named colour palettes, plus prompt-driven automatic selection
- Fourteen aspect/resolution combinations up to 1280 px on the long edge
- Manual override of detail, distortion, contrast, grain and vignette
- Seed control with lock, randomise and rebuild
- Five restyle treatments: Duotone, Palette Reduction, Posterize, Contour, Halftone
- Real, cancellable, progressive rendering with honest progress reporting
- Full-resolution PNG export for both workflows
- Session history of the current sitting

## Technologies

- TypeScript
- React
- Canvas 2D
- Vite
- Tailwind CSS

## Running locally

Requires Node.js 18 or newer.

```bash
npm install
npm run dev
```

The development server starts on the printed local URL.

### Production build

```bash
npm run build
npm run preview
```

## Project layout

```
src/
  App.tsx                 application shell, navigation, section composition
  index.css               design tokens and base styles
  components/
    Hero.tsx              opening section with live engine previews
    Studio.tsx            prompt → image workspace
    Restyle.tsx           image → image workspace
    Sections.tsx          objective, how it works, technology, limitations, footer
    LivePreview.tsx       small real-time renders used for engine selection
    ui.tsx                shared interface primitives
    icons.tsx             inline icon set
  lib/
    noise.ts              seeded PRNG, Perlin noise, fBm, ridged noise, Worley noise
    engines.ts            structure definitions and field functions
    palettes.ts           palette table and colour ramp lookup
    prompt.ts             prompt keyword lexicon and interpretation
    render.ts             progressive renderer and finishing pass
    imageops.ts           image measurement and pixel treatments
    media.ts              aspect/resolution helpers and PNG export
    examples.ts           sample prompts and default tone
```

## Determinism

Given the same prompt, seed, structure, palette and tone settings, the renderer always
produces the same image. This makes every result citable and reproducible.

## Limitations

- The prompt reader works with descriptive words, not meaning. It cannot draw a specific
  subject — "a red bicycle" will not produce a bicycle.
- There is no neural network and no training data. Images are synthesised from mathematical
  fields, so results are abstract rather than photographic.
- Large renders at high detail take a few seconds because every pixel is computed on the spot.
- Restyle treatments operate on pixels only; they cannot move, remove or redraw content.

## Responsible use

Generated images are original compositions produced from mathematical fields, not from a
corpus of existing artwork. No image uploaded to the restyle workspace leaves the device.
