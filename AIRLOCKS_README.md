# Airlock Systems

## Programs

- `RegularAirlock.ic10`: simple direct-device airlock using one vent and interior/exterior doors.
- `StateMachineAirlock.ic10`: core pressure-driven state machine using hashed door devices.
- `StateMachineAirlockController.ic10` + `StateMachineAirlockActuator.ic10`: split controller/actuator design. The controller reads the button and pressure; the actuator applies door and vent outputs.
- `StateMachineAirlockControllerHumanTrap.ic10` + `StateMachineAirlockActuatorHumanTrap.ic10`: trap-mode variant. The controller can bypass pressure waits and the actuator forces vents off in trap mode.
- `StateMachineAirlockDeviceRef.ic10`: direct `d0`-`d4` door/vent/sensor references; the button remains hash-operated and self-resets.
- `linked list controller/StateMachineAirlockControllerLinkedList.ic10`: controller variant that delegates device-list work to the linked-list service.

## Setup

The state-machine pair normally needs interior and exterior vents, a gas sensor, two doors, a button, and a controller memory channel. Hash-based variants require matching device names and button/door hash defines. The device-reference version expects `d0`-`d4` to be wired in the order documented by its aliases.

Run the controller and actuator together when using the split design. The controller publishes the current state; the actuator owns physical outputs. Keep the human-trap controller and actuator paired.

## Safety

Set pressure thresholds for the room and suit environment before enabling the doors. Test each state with doors disabled, then verify that a failed sensor or disabled controller leaves vents and doors in a safe state.
