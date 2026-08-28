# Utility Scripts

- `DoorPressRead.ic10`: reads a door control and writes a debounced pulse to the door setting. Useful for turning a lever-style input into a single action.
- `weatherConsole.ic10`: reads a weather station, controls a storm switch and flashing light, and selects speaker mode. Boolean flags are multiplied into mode values; bitwise `and` must not be used as a general gate.
- `weatherTest.ic10`: currently an empty placeholder and has no runtime behavior.
- `SateliteDishCOnReference.ic10`: integrated reference implementation for mode-based satellite-dish broad and narrow sweeps.
- `SateliteDishSignalDisplayStack.ic10`: stores the best dish signal snapshot and writes horizontal, vertical, and signal values to displays.

Check aliases and any hash-based names in each file before wiring. The satellite display script is normally used alongside a dish controller, while the reference script is useful as a single-chip starting point.
