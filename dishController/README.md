# Satellite Dish Controller

These scripts split dish operation into a mode router and two workers so each chip stays small and focused.

- `SateliteDishModeRouter.ic10`: reads the mode dial and publishes the selected mode to the shared queue.
- `SateliteDishBroadSweep.ic10`: performs broad sweeps for automatic broad modes.
- `SateliteDishNarrowSlope.ic10`: performs fine narrow sweeps around a target center.

The shared queue uses mode slot `2`, horizontal center slot `3`, and vertical center slot `4`. The router maps dial ranges to modes; both workers read the published mode and remain idle when it does not apply to them. The narrow worker also uses a setpoint display and waits between adjustments.

Run the router and the relevant worker with the same shared memory device. Add `SateliteDishSignalDisplayStack.ic10` when a best-signal snapshot is needed.
