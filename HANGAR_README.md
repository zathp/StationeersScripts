# Hangar Door Air Cycle

## Programs

- `HangarDoorAirCycleController.ic10`: detects the mode lever edge and advances the hangar cycle state.
- `HangarDoorAirCycleActuator.ic10`: applies door, vent, and pump outputs for the published state.
- `HangerDoorAirCycleControllerHumanWritten.ic10`: hand-written controller variant for comparison or experimentation.
- `HangarStatusDisplay.ic10`: displays state with text and color.
- `HangarDoorStatusConsole.ic10`: alternate console text output.
- `HangarPressureLedController.ic10`: standalone pressure-to-LED indicator.

## Setup

The controller and actuator are intentionally split because the complete air-cycle behavior can exceed the IC10 instruction limit. Run both chips and connect their shared state memory. Add the status display or console as a separate consumer of controller state.

The mode lever is treated as a rising-edge trigger for starting the close and pressurize sequence. The pressure LED uses separate depressurized and pressurized targets; set those defines to match the hangar volume and operating atmosphere.

Test the actuator with the doors mechanically isolated before enabling a full cycle.
