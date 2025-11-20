Ans:

Because browsers map CSS pixels to device pixels and round fractional
positions, a 1px-high element can end up on a half‑device‑pixel boundary
depending on the computed offsets. With three 1px lines and a particular
margin, the middle line’s y position can fall on a fractional pixel for
some margin values (often when the sum/offset parity changes), so the
renderer rounds differently and that line looks thinner. Odd vs even
margins change the resulting offsets and whether they land on integer
device pixels.

Quick fixes (pick one):

Force vertical stacking and avoid flex-wrap (makes positions
deterministic).
Make the spans display:block and ensure margins/heights produce integer
positions.
Use a 2px line or a 1px border (borders tend to be rendered more
consistently).
As a last resort, use transform: translateZ(0) / will-change to trigger
layer compositing (can hide rounding artifacts, but is a workaround).
