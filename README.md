# Fluid_flow_simulation

**Plate Port Flow Lab** is an interactive simulation of hot water flowing across one channel of a gasketed plate heat exchanger.

Open `index.html` in a browser. It is a single file with no build step and no dependencies.

## Open it from GitHub (GitHub Pages)

Once GitHub Pages is switched on, the simulation is live at:

**https://kashyap10anirudh.github.io/Fluid_flow_simulation/**

To switch it on (one time):

1. On GitHub, open the repository and go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose the branch that holds `index.html` (`main` once this work is merged, or `claude/plate-port-flow-lab` until then) and the folder **/ (root)**. Then click **Save**.
4. Wait a minute or two. The address above appears at the top of the Pages settings when it's ready.

GitHub Pages for a **private** repository needs a paid GitHub plan (Pro, Team or Enterprise). On a free plan, make the repository public first (**Settings → General → Danger Zone → Change visibility**). The empty `.nojekyll` file tells Pages to serve the files as they are.

## What it does

- **The plate:** 200 × 440 mm and 0.5 mm thick. The hot-side inlet and outlet ports are on the right, the sealed cold-side ports with ring gaskets on the left, and a diagonal channel gasket runs around them.
- **The flow:** water enters through the inlet port at a constant speed, or at a constant flow rate if you choose. It spreads into the channel, runs down the plate and leaves through the outlet port.
- **Defaults:** Ø35 mm ports, a 2 mm pressing depth (channel gap), 1 m/s port velocity, and 50 channels fed by the port. In a plate pack every second gap carries the hot water, so the port flow is shared between all those channels. The page simulates one of them, which gets `Q = v_port × A_port / 50`, about 1.2 L/min. The simulation runs faster when the flow is slow, so slow designs still settle within seconds.
- **Distribution areas** under each port fan the flow across the plate width before it reaches the heat transfer area. You can turn them on or off and set their length.
- **Chevron (herringbone) ribs** in the heat transfer area resist sideways flow, stir the water and raise heat transfer. You can turn them on or off and set the chevron angle from 10° to 80°. Use the slider, the soft (30°), mixed (45°) and hard (60°) presets, or drag the angle handle on the plate.
- **The gasket** has straight side seals with rounded transitions into the diagonal sections. When you edit the gasket line, side points snap back into line so the sides stay straight.
- **Port shapes** can be changed with presets (circle, square, slot, teardrop, D-shape, diamond), sliders (size, aspect, rotation) or by dragging 16 handles on the outline. You can also move the ports and edit the gasket line.
- **Views:** colour the plate by speed, pressure, temperature, heat transfer coefficient, fluid age or swirl. Particles, streamlines and arrows can be shown on top.
- **Readouts:**
  - Hydraulics: channel flow, pressure drop, Reynolds number, mean speed and low-flow area.
  - Heat transfer: outlet temperature, heat duty, mean U and effectiveness.
  - A profile across a movable section A–A. Pick downward, sideways or overall speed, pressure, temperature, heat transfer coefficient, fluid age or swirl from the drop-down. A flow-uniformity index is always shown.
- **Comparison:** pin a design as a reference and every readout and the A–A profile show the difference.

## Model

- 2-D incompressible flow averaged across the channel gap, solved on a 2 mm grid. It uses a staggered (MAC) grid, semi-Lagrangian advection, implicit wall friction and a friction-weighted SOR pressure projection.
- **Flat areas** use Hele-Shaw friction `12 μ / h²`, where `h` is the channel gap (0.5–5 mm).
- **Chevron areas** use Martin's friction factor and Nusselt correlation (VDI Heat Atlas), evaluated from the local Reynolds number and the angle between the local flow and the ribs on each of the two walls.
- **Distribution areas** are triangles under the diagonal gaskets, as on real plates. They carry an open "chocolate" stud pattern, which plate patents describe as having few, large contact points and low resistance. It's modelled as resisting flow equally in every direction, using Martin's correlation at an effective 25°. That 25° is an assumption, not a published value.
- **Particles in the ribbed area** travel in two layers, one near each plate, that follow that plate's ribs. They hand over to the facing plate where the streams cross, at the herringbone apex and at the gasket, as flow-visualisation studies of cross-corrugated channels show. The two layers average to exactly the computed flow, so the criss-cross is shown without changing the flow.
- **Heat transfer:** the cold side is held at a constant temperature with the same film coefficient as the hot side. `1/U = 2/h + t/k_steel`, so plate thickness enters through wall conduction (AISI 316, k = 16 W/m·K).
- **Port flow:** `Q = v_port · A_port / N_channels`, spread evenly over the inlet port area and removed over the outlet port area.

## Editing

`src/page.html` is the source. Run `src/build.sh` to regenerate the standalone `index.html`.
