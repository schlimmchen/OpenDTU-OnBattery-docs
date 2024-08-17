# Introduction

The dynamic power limiter (DPL) is a software feature allowing automatic
inverter power limit adjustments. Depending on the serup, the DPL will take the
power meter (i.e. currently consumed power), the available solar power, and the
battery charge state into account. The inverter is steered such that the
currently consumed power (as provided by the power meter) reaches a
user-defined value (usually zero). In particular, this allows to implement a
zero export setup.

!!!note "Systems without battery"
    The DPL also works in systems that do not have a battery, i.e., where the
    inverter is powered by solar panels directly.
    [Configure](configuration/dpl.md) the DPL accordingly. Battery-related
    features and settings do not apply for these setups.

!!!note "Systems without a power meter"
    Setups without access to a power meter reading are supported. However, this
    implies that the inverter will never produce more than the configured base
    load.

Refer to the documentation on [DPL parameters](configuration/dpl.md) to learn
how to configure the DPL.

## Terminology and Basics

!!!warning "Best Effort"
    The DPL can be slow (>10 seconds) to calculate and send a new power limit.
    With tuning, the limit updates can be as frequent as one or two seconds.
    There will always be a delay. The DPL **cannot** be expected to react in
    "realtime" similar to a commercial inline battery/inverter combination.

### Inverter

The DPL is currently capable of controlling a single inverter only.

It is expected that the DPL is in exclusive control over the inverter. No other
software and no human interaction shall trigger limit updates to be sent to the
inverter.

### Battery Cycles

!!!note "Reboot State"
    After a reboot the battery is assumed to be in a charge cycle unless the
    SoC or voltage is found to be above the respective start threshold.

#### Charge Cycle

A battery charge cycle is started when the battery SoC or voltage falls below
the respective stop threshold. The charge cycle completes when the battery SoC
or voltage reaches the respective start threshold.

#### Discharge Cycle

The battery is or was charged to or beyond the start threshold. The discharge
cycle ends when the battery SoC or voltage reaches the respective stop
threshold.

### Voltage Measurements

If the DPL is configured such that voltage thresholds (rather than SoC
thresholds) are effective, the voltage reading is taken from any of the
following sources, in the given order:

1. [Battery interface](battery_interface.md)
2. [Victron charge controller](../hardware/victron_charge_controllers.md)
   battery output terminal
3. Selected inverter input (configurable)

If available, the battery interface voltage reading is preferred, as it is
closest to the actual battery and therefore to be expected to be the most
accurate. Without a battery interface and if available, the victron charge
controller output voltage is preferred, as it also is often closer to the
battery as well as more accurate. As a fallback, the inverter's input voltage
reading is assumed as the battery voltage.

### (Full) Solar-Passthrough

If the currently available solar power is known, the DPL can make additional
decisions on how to calculate the inverter limits. See the documentation on
[(Full) Solar-Passthrough](solar_passthrough.md).
