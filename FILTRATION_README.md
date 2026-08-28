# Filtration Systems

## Programs

- `FiltrationCO2O2Control.ic10`: enables filtration when CO2 rises and protects against low O2.
- `FiltrationPressureIdle.ic10`: runs a filter with pressure-based PWM below the target and idles above it.
- `FiltrationLiquidPollutantThreshold.ic10`: enables an output when liquid pollutant exceeds its threshold.
- `FiltrationPercentConrtol.ic10`: checks up to seven filtration units and tracks gas ratios.
- `FiltrationFlashingLight.ic10`: flashes an alarm when both secondary atmosphere quantities are low.

## Configuration

Important defines include `Co2RisePct`, `O2BasePct`, `TargetPressure`, `PressureBand`, `PwmPeriod`, `PollutantThresholdPct`, and `NumFiltration`. Set these for the actual room, pipe, and filtration count.

Connect the output device expected by each program and verify whether it uses a direct alias, a hash, or a database channel. Threshold scripts without hysteresis can chatter near the limit; add operating margin through the configured threshold or external control logic.
