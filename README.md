# Fluid_flow_simulation

**Plate Port Flow Lab** is an interactive simulation of water flowing across one channel of a gasketed plate heat exchanger.

Open `index.html` in a browser. It is a single file with no build step and no dependencies.

## What it does

- A 200 × 400 mm plate (0.5 mm thick) with an inlet port at the top right, an outlet port at the bottom right, and a gasket that seals the channel.
- Water enters through the inlet port at a constant speed, spreads into the channel, runs down the plate and leaves through the outlet port.
- Reshape either port with presets (circle, square, slot, teardrop, D-shape, diamond), sliders (size, aspect, rotation) or by dragging its 16 control handles. You can also move the ports and edit the gasket line.
- See the flow as speed, pressure, swirl (vorticity) or fluid age, with particles, streamlines and arrows on top.
- Readouts: channel flow, pressure drop, Reynolds number, low-flow area, nominal residence time, and a velocity profile across a movable section A–A with a flow-uniformity index.

## Model

- 2-D incompressible flow averaged across the channel gap, solved on a 2 mm grid. It uses a staggered (MAC) grid, semi-Lagrangian advection and a SOR pressure projection.
- Hele-Shaw wall friction `12 μ / h²` stands in for the two plate walls. `h` is the channel gap, which you can set from 0.5 to 5 mm.
- The port flow `Q = v_port · A_port / N_channels` is spread evenly over the inlet port area and removed over the outlet port area.
- The plate is flat, with no chevron corrugations. Plate thickness sets the plate pitch shown in the cross-section; it does not affect the in-plane flow.

## Editing

`src/page.html` is the source. Run `src/build.sh` to regenerate the standalone `index.html`.
