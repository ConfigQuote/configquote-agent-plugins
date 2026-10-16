---
name: generate-3d-model
description: Generate a parametric 3D model from a text description and store it in the tenant's ConfigQuote model library. Supports implicit.js SDF models (browser-native, no backend) and STEP/GLB models (via text-to-cad coding agents). Returns viewer and model URLs.
---

# Generate 3D Model

Generate a parametric 3D model for a ConfigQuote tenant and attach it to a configurator node.

## When to use

- User asks to "add a 3D model", "generate a part", "create a parametric shape", or describes a product geometry
- User wants to replace the existing 3D viewer in a configuration with an agent-generated model
- User wants to visualise a product configuration step with a 3D preview

## Approach — Track B (Claude: implicit.js, no Python environment)

Claude generates a `.implicit.mjs` ES module defining the geometry as a signed-distance function (SDF). This runs entirely in the browser via WebGL — no server-side Python is required.

### implicit.js module structure

```js
// Required: default export is the SDF function (signed distance from point to surface)
export default function sdf(x, y, z, params) {
    // Return distance to surface (negative = inside)
    const r = params.radius ?? 1.0;
    return Math.sqrt(x*x + y*y + z*z) - r;
}

// Required: bounding box for the model
export const bounds = { min: [-2, -2, -2], max: [2, 2, 2] };

// Optional: expose interactive parameters
export const parameters = [
    { name: 'radius', type: 'number', default: 1.0, min: 0.1, max: 5.0, label: 'Radius' },
];

// Optional: animation keyframes
export const animation = {
    duration: 2000,
    keyframes: [
        { t: 0, params: { radius: 0.5 } },
        { t: 1, params: { radius: 2.0 } },
    ],
};
```

### Steps

1. Write the `.implicit.mjs` module code for the described geometry (spheres, boxes, cylinders, unions, intersections, subtractions are all expressible as SDF operations)
2. Call `create_implicit_model` with the code and a descriptive name
3. The tool returns `model_url` and `viewer_url`
4. Optionally call `update_configuration` to bind `model_url` into a `node-implicit-viewer` node's data

## Approach — Track A (Codex/Antigravity: text-to-cad, Python + build123d)

If running as a coding agent with a Python environment and the text-to-cad skill installed:

1. Write a `build123d` Python source file for the described geometry
2. Run `python skills/cad/scripts/step <source.py>` to produce STEP + GLB artifacts
3. Base64-encode the output file and call `upload_model` with `filename` set to the `.step` or `.glb` name
4. Use the returned `model_url` in a `node-cad-viewer` configurator node

## Defaults

- Prefer `create_implicit_model` when no Python environment is available (Claude, ChatGPT)
- Use `upload_model` when a compiled STEP or GLB file is available (Codex, Antigravity, local Claude Code)
- Always set a human-readable `name` that reflects the part geometry
- Do not upload files larger than 100 MB
- Check `list_models` first if the user says a model already exists
