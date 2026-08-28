# Hydroponics Natural Selection

## Programs

- `HydroLarreNaturalSelPt1.ic10`: scans trays and queues harvest positions.
- `HydroLarreNaturalSelPt2.ic10`: consumes the queue, performs the harvest, and replants.

Run Part 1 and Part 2 as a pair with shared database memory. The current tray convention is `basePos + 1` through `basePos + NumTray`, inclusive.

Part 1 publishes the shared values below:

- `db255`: number of trays
- `db254`: base position
- `db253`: harvest/dropoff position (`harv`)
- `db252`: seed pickup position (`pick`)

Keep harvest and pickup positions separate. Configure `NumTray`, `basePos`, `harv`, and `pick` consistently in both programs before enabling the larre.
