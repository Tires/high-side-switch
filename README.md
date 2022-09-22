# High side switch

Circuit for high side switch 60V up to 3 kW

# Requirements

The power supply of a motor controller should be switched on the high side (Vss). The operating voltage (Vss) with a low current in the maximum range of a few milliamps is used as the switching signal. In contrast to other so-called anti-spark switches, the high-side switch is switched off when the input is open. Therefore, only a single closer is required. The switching line can also be connected to dependent signaling devices.

# Why High Side?

If the low side is switched, the electronics are still dependent on the operating voltage. Current continues to flow through components connected to ground. This leads to unpleasant side effects, permanent power consumption, etc.

# Features

* Current up to more then 100 Amperes (need cooling)
* Clipping battery connecting spikes
* Clipping switching on/off spikes
* Support recuperation (with diode of Mosfet)
* Single control input wire
* Pass through ground
* Simple, available components
* Minimal to no power consumption in off state

# Notes on the Circuit Diagram

In LTSpice I didn't have the exact components used, so I used similar components.

The following components have been tested in practice up to 3 kW:

| Component | Type |
| --------- | ---- |
| T1-T4 | SPP80P06PH, Infineon, P-Channel, -60V, -80A, 0.023R |
| T5 | 2N5551, NPN transistor, 160V, 0.6A, 0.63W |
| D1 | Generic Zener Diode, 15V, 0.5W |
| D2 | P6KE56CA, TVS suppressor diode, 56V, 600W |
| R[x] | Resistor 1/4 watts |
| C2 | 220nF, 1ß0V, polyester (20V is also sufficient) |

The rest of the wiring is only for simulation.

# Simulation

1. At 1s the supply voltage 54.6V (=Li-Ion 13S) is switched on. Only an almost invisible spike can be seen through capacitances in the picofarad range.
2. At 2s the control line is set to high. The load capacitor of 100uF is loaded. The delayed increase in voltage at the Mosfets extends the switch-on process by a few milliseconds. This keeps the current below 50A. If that is still too much for you, you can also use 1uF for C2.
3. At 3s, a sinusoidal load is switched on, which alternately draws up to approx. 1.5kW of power and then recuperates slightly.
4. At 7s, the load is cut off.
5. At 8s the control line becomes highly resistive. After C2 is discharged above 200K, the mosfets turn off.
6. At 9s the supply voltage is switched off.

# Evaluation

All parameters remain within specification. The maximum power at all 4 Mosfets together is approx. 20 watts if power peaks of 1.5kW are requested at the consumer. For this purpose, the 4 Mosfets were additionally mounted on a small heat sink (see photo).

# Outlook

You could also use 6 mosfets of type SPP80P06PH. For new projects with even higher power consumption, a high-side switch with N-channel mosfets may be implemented. Unfortunately, corresponding components are now difficult to obtain in some places.