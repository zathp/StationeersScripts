# PID and Process Control

## Programs

- `CounterFlowPID.ic10`: temperature PID for a counter-flow pipe cooler. `d0` pauses, `d1` is the pipe analyser, and the pump is the output device.
- `EvaporationChamberPID.ic10`: adjusts chamber pressure to hold a target temperature; lower pressure generally increases evaporation.
- `EvaporationChamberPIDBatch.ic10`: one-shot evaporation cycle with idle, run, settle, and complete states.
- `GasMixerPID.ic10`: adjusts a gas mixer setting from analyser temperature feedback.
- `ValveRoomPipeTempControl.ic10`: simple hysteresis valve control; it is not a PID loop.
- `PipeFillCoolStateMachinePID.ic10`: fills a pipe, cools it to a target, waits for settling, and pumps it out.
- `StirlingRoomRadiatorControl.ic10`: retains the Stirling fill/run/drain cycle and independently controls room radiator circulation and draining at 283.15 K (10 C).
- `DualPumpLiquidMixerPID.ic10`: splits total liquid flow between two pumps using a ratio PID and total-moles correction.
- `BatteryChargeTransformerPID.ic10`: holds the network-average charge of all Large Station Batteries at 50% by adjusting a Transformer's `Setting`; auto-pauses (transformer off) above 55% charge and resumes once it drops back below 53%.

## Tuning

Review the `define` block before loading. Common values include `TargetTemp`, `TargetPressure`, `Kp`, `Ki`, `Kd`, `TickSeconds`, output limits, and integral clamps. Start with a low output limit and raise it after confirming sensor direction and actuator direction.

`DualPumpLiquidMixerPID.ic10` uses `d0` enable, `d1` ratio sensor, `d2` PumpA, and `d3` PumpB. Its ratio mode is selected from the stacked `LogicType` values near the top of the program. `TargetRatio` controls PumpA's share and `TotalFlowSetting` is corrected toward `TargetTotalMoles`.

Paused modes in the PID scripts should turn outputs off while retaining controller state where implemented. Confirm this behavior in a test setup before connecting production equipment.

## Stirling with room radiator control

[StirlingRoomRadiatorControl.ic10](StirlingRoomRadiatorControl.ic10) is a separate version of [StirlingStateMachine.ic10](StirlingStateMachine.ic10); the original is unchanged. Both control routines run once per loop, so waiting for either pipe system never blocks the other.

Keep the original Stirling wiring: `d0` import pump, `d1` export pump, `d2` Stirling pipe analyser, and `d3` supply pipe analyser. Connect a room gas sensor to `d4`; `d5` is unused. The original Stirling prefab-wide control remains, so every Stirling engine on the data network is still controlled together.

Use standard **gas** devices on the same data network and name them exactly as follows (both devices in each group share the same name):

| Devices | In-game name |
| --- | --- |
| Two digital gas valves feeding the radiator sections | `Room Radiator` |
| Two gas volume pumps circulating/draining those sections | `Room Radiator` |
| Two gas pipe analysers, one on each radiator section | `Room Radiator` |

These names must be unique to this radiator system. Install and connect both analysers; the script uses the maximum reading of all matching analysers, not a sum. Set pump direction and flow `Setting` manually: the script only controls `On`. Closing the valves must isolate the gas supply while leaving each pump a path to empty its radiator section.

- **Room above `RoomTargetK` (default 283.15 K):** both valves open and both pumps run, even when the radiator pipes are empty.
- **Room at or below target:** both valves close first. Both pumps continue running while the maximum analyser `TotalMoles` is **at least 2**. Both stop only when that maximum is **strictly below 2**; there is no separate pressure-based cutoff.
- **Room warms above target during draining:** both valves reopen and both pumps circulate immediately, without waiting for draining to finish.
- **Room above `StirlingRoomMaxK` (default 303.15 K / 30 C):** the Stirling engine is forced off. Radiator cooling and the Stirling fill/drain state machine continue normally. When the room returns to or below the limit, the engine may run again if the Stirling cycle is in its run state; no manual reset or hysteresis is used.
- There is no hysteresis, and neither loop changes the other's state. Below target, residual gas reaching 2 moles in either section restarts both drain pumps.

Adjust `RoomTargetK`, `StirlingRoomMaxK`, `EmptyMoles`, or the name hashes before loading if needed. The Stirling thresholds are 5000 kPa supply pressure, 30000 kPa fill pressure, 293.15 K run cutoff, and 50 moles drain cutoff.
