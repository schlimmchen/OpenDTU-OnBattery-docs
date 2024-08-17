# (Full) Solar-Passthrough

## Solar-Passthrough

Solar-Passthrough is a feature that, if enabled, makes the [DPL](dpl.md)
calculate an inverter limit such that the available solar power is first used
to cover the needs of the household. This effectively prevents the energy from
being stored in the battery just so it can be discharged later. If there is any
surplus solar power left, it will be used to charge the battery.

Refer to the [DPL documentation](dpl.md) to understand what is considired a
battery charge and discharge cycle.

### Solar-Passthrough is OFF

* The inverter is disabled during a battery charge cycle.
* All solar power will be used to charge the battery.
* The inverter is enabled during a battery discharge cycle.
    * The inverter will use as much power as is needed to compensate the
      household consumption.
    * Depending on the current consumption and the available solar power, the
      battery is drained.

### Solar-Passthrough is ON

As with Solar-Passthrough OFF, in general the inverter is disabled during a
battery charge cycle, and it is enabled during a battery discharge cycle.

With Solar-Passthrough ON, there is an important difference while the battery
is in a charge cycle:

* If there is solar power available (Victron MPPT is producing power), it will
  be used to cover the household consumption.
    * The inverter is thus enabled and producing power even though the battery is
      in a charge cycle.
    * The inverter power limit is **constrained to the solar power**. Therefore,
      discharging of the battery is avoided.
* Surplus solar power (available when solar output is greater than the
  household consumption) still charges the battery.

## Full Solar-Passthrough

There is an additional battery SoC/voltage threshold activating **Full**
Solar-Passthrough.

While the battery reached or is above the **Full** Solar-Passthrough threshold,
the inverter's limit is set to match the total solar power output (regardless
of the power meter value). This threshold is usually configured such that Full
Solar-Passthrough activates when the battery is considered fully charged.
Surplus solar power is then fed into the grid.

!!!note "Limitation"
    If the solar output power is greater than the inverter can feed into the
    grid, the charge controller will eventually switch to absorbtion and then
    float mode. This reduces the charge controller's power output, and the
    inverter follows the new output power, and the production of AC power
    seizes.
