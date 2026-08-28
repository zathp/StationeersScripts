# Stationeers IC10 Scripts

A collection of IC10 programs for Stationeers automation. Scripts are grouped by the system they control; the `.ic10` files remain at their existing paths.

## Guides

- [Airlocks](AIRLOCKS_README.md): regular, state-machine, human-trap, device-reference, and linked-list airlocks.
- [PID and Process Control](PID_README.md): temperature, pressure, gas mixing, evaporation, and pipe state machines.
- [Filtration](FILTRATION_README.md): gas composition, pressure, pollutant, and atmosphere alarms.
- [Hangar Door](HANGAR_README.md): controller, actuator, status displays, and pressure indication.
- [Rocket Systems](ROCKET_README.md): countdown/descent calculations, pump control, and boiloff pressurization.
- [Logistics and Furnaces](LOGISTICS_README.md): arc furnaces, sorters, stackers, and printer output routing.
- [Hydroponics](HYDROPONICS_README.md): two-chip natural-selection harvest workflow.
- [Utilities](UTILITIES_README.md): door input, weather, and satellite display helpers.
- [AutoPrinter](AutoPrinter/README.md): deque workers, printer requests, silo routing, and import handling.
- [Satellite Dish Controller](dishController/README.md): split broad-sweep, narrow-sweep, and mode-router workers.
- [Linked List Controller](linked%20list%20controller/README.md): stack-based linked-list service and helper routine.

## IC10 conventions used here

- Most programs use `d0`-`d6` aliases for directly connected devices.
- Larger systems use hashed device names with `lbn`/`sbn`, or ReferenceId values written through stack commands.
- IC10 programs in this repository are kept within registers `r0`-`r15`.
- LogicType values that need to be selected at runtime are stored with `push` and read with `peek`.
- Use `mul` to gate a value by a boolean. `and` is bitwise and is not a general boolean gate.
- Use a named negative constant instead of inline negation when the IC10 parser rejects forms such as `-IntegralClamp`.

## Installation

Copy the required `.ic10` file to an IC Housing or IC Editor, then connect the devices named in its guide. Hash-based scripts require the in-game device names to match the hashes used by the program. Adjust `define` values in the source before loading when a target pressure, temperature, hash, or slot layout differs.

These scripts are automation components, not a universal plug-and-play package. Test pumps, heaters, doors, and pressure systems with conservative limits first.
