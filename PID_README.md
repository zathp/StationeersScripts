# PID and Process Control

## Programs

- `CounterFlowPID.ic10`: temperature PID for a counter-flow pipe cooler. `d0` pauses, `d1` is the pipe analyser, and the pump is the output device.
- `EvaporationChamberPID.ic10`: adjusts chamber pressure to hold a target temperature; lower pressure generally increases evaporation.
- `EvaporationChamberPIDBatch.ic10`: one-shot evaporation cycle with idle, run, settle, and complete states.
- `GasMixerPID.ic10`: adjusts a gas mixer setting from analyser temperature feedback.
- `ValveRoomPipeTempControl.ic10`: simple hysteresis valve control; it is not a PID loop.
- `PipeFillCoolStateMachinePID.ic10`: fills a pipe, cools it to a target, waits for settling, and pumps it out.
- `DualPumpLiquidMixerPID.ic10`: splits total liquid flow between two pumps using a ratio PID and total-moles correction.
- `BatteryChargeTransformerPID.ic10`: holds the network-average charge of all Large Station Batteries at 50% by adjusting a Transformer's `Setting`; auto-pauses (transformer off) above 55% charge and resumes once it drops back below 53%.

## Tuning

Review the `define` block before loading. Common values include `TargetTemp`, `TargetPressure`, `Kp`, `Ki`, `Kd`, `TickSeconds`, output limits, and integral clamps. Start with a low output limit and raise it after confirming sensor direction and actuator direction.

`DualPumpLiquidMixerPID.ic10` uses `d0` enable, `d1` ratio sensor, `d2` PumpA, and `d3` PumpB. Its ratio mode is selected from the stacked `LogicType` values near the top of the program. `TargetRatio` controls PumpA's share and `TotalFlowSetting` is corrected toward `TargetTotalMoles`.

Paused modes in the PID scripts should turn outputs off while retaining controller state where implemented. Confirm this behavior in a test setup before connecting production equipment.
