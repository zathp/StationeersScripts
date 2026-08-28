# Rocket Systems

## Programs

- `RocketConCountdown.ic10`: reads avionics state and thrust command, then derives descent speed from altitude change per tick.
- `RocketConPumpControl.ic10`: converts thrust demand into pump settings and regulates feed pressure with a PID loop.
- `RocketConBoiloffPressurization.ic10`: preheats helium and controls liquid-line pressurization and pump duty.
- `RocketConBoiloffPressurizationPID.ic10`: variant of the boiloff controller that replaces the heater on/off latch with a PID driving `HeliumHeater Setting`, and drives both feed pumps from a pressure PID whose setpoint is mapped directly from `ThrustCmd` (no separate `HeliumPipe` analyser; heater reports its own `Temperature`, freeing a pin for `ThrustCmd`).

## Configuration

Set maximum thrust, pressure targets, pressure bands, tick interval, and heater temperature limits in each `define` block. The boiloff controller uses a heater latch between `MinHeliumTemp` and `MaxHeliumTemp` and pressure-based pump PWM. The PID variant instead uses `TargetHeliumTemp` with `HeaterKp/Ki/Kd` for the heater and `MaxLinePressure`/`MaxThrustN` with `PressureKp/Ki/Kd` for the pumps.

The countdown script uses altitude delta because the available Avionics logic fields in this setup do not expose a usable speed field. Validate the sign convention and tick interval on the actual vehicle before relying on descent calculations.

Rocket automation can create dangerous pressure and thrust changes. Test with low limits and an independent shutdown path.
