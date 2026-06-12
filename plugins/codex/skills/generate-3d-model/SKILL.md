---
name: generate-3d-model
description: Generate a 3D model using the text-to-cad skill (build123d / OpenCascade) and upload it to the tenant's ConfigQuote model library. Returns viewer and model URLs that can be bound to a node-cad-viewer configuration node.
---

# Generate 3D Model (Codex — Track A)

Generate engineering-grade CAD from a text description using build123d (OpenCascade) and upload it to ConfigQuote.

## When to use

- User asks to "add a 3D model", "generate a STEP file", "create a parametric bracket/housing/etc."
- User wants to attach a STEP or GLB model to a configurator node
- User wants animation or assembly structure (use STEP + cad-viewer)

## Steps

1. **Install text-to-cad skill** (if not already installed):
   ```
   npx skills add earthtojake/text-to-cad
   ```

2. **Write build123d Python source** — create a `.py` file with build123d geometry. Use parameters for configurability:
   ```python
   from build123d import *
   
   width = 50  # @param width: float = 50
   depth = 30  # @param depth: float = 30
   height = 20 # @param height: float = 20
   
   box = Box(width, depth, height)
   export_step(box, 'output.step')
   ```

3. **Generate STEP + GLB**:
   ```
   python skills/cad/scripts/step output.py
   ```
   This produces `output.step` and `.output.step.glb` (with topology).

4. **Upload to ConfigQuote** — base64-encode and call `upload_model`:
   ```python
   import base64
   with open('output.step', 'rb') as f:
       encoded = base64.b64encode(f.read()).decode()
   # Then call upload_model MCP tool with file=encoded, filename='output.step'
   ```

5. **Bind to configuration** — use the returned `model_url` in a `node-cad-viewer` node via `update_configuration`.

## Supported output formats

STEP, STP, STL, 3MF, GLB, DXF, URDF, SRDF, SDF — all accepted by `upload_model`.

## Defaults

- Always produce a STEP file for engineering models (topology + animation support)
- Include a GLB sidecar (produced automatically by `scripts/step`) for fast browser preview
- Max upload size: 100 MB (base64-encoded)
- For simple SDF parametric models without a Python environment, use `create_implicit_model` instead (Track B — see Claude plugin skill)
