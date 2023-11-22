# SASI Switcher
 A circuit to switch between analog and digital 2-axis control, leaving either in a prescribed inactive state.


## Project Goals

The SASI Switcher circuit is intended to switch between the ability to control a two axis analog device and a four input digital device. Versions 0.0 and 1.0 are currently intended to be only passthroughs, allowing the intended signal to pass while the unwanted signal will return to an inactive state. For versions 0.0 and 1.0, the inactive state will be the center supply voltage for both analog axes and open circuits for all four digital inputs. The circuit will activate one input and deactivate the other simultaneously. Except for the switching time, the analog and digital inputs cannot be passed through simultaneously. 

The SASI Switcher aims to resolve this problem at the lowest cost with the widest availability, compatability, manufacturability, and adaptability (should a component cease production).

-----

## Project I/O
The "Panel" of the SASI Switcher are as follows:

* 4 pin analog VCC, GND, Y, X

* 5 pin digital Up, Down, Left, Right, GND (pin order tbd)

* 2 pin digital "mode switch" to switch between analog and digital passthrough

The "Control Board" of the SASI Switcher are as follows:

* 4 pin analog VCC, GND, Y, X

	* The "Control Board" connectors of the SASI Switcher are to supply the VCC and GND to the SASI Switcher, even though the Y and X values are output from the SASI Switcher to the Control Board.

* 5 pin digital Up, Down, Left, Right, GND (pin order tbd)

Internally, the SASI Switcher features or resembles the following:

* 2 Channel DPST/2:1 Analog MUX for analog control

	* Active state passes through the "Panel" Analog

	* Inactive state uses a tunable center voltage per axis

* 4 Channel SPST Switching IC for digital control

	* Active state passes through the "Panel" 5 pin digital

	* Inactive state uses a pull up resistor to VCC or remains floating through the IC impedance

		*A pull up resistor is desirable, but it may unexpectedly interfere with the control board if the SASI Switcher VCC and control board button pull up are differing voltages

* "Default Mode" Jumper to switch between defaulting to analog active or digital active when the "mode switch" is not closed
	* could possibly invert the "mode switch" line

-----

## Project Implementation
The project *must* be capable of both 3.3V and 5V VCC input.

The design can be either separated into analog and digital circuits OR it can be combined into a single analog MUX circuit with at least 6 DPST channels.

<<<<<<< Updated upstream
=======
<<<<<<< HEAD
	| Chip Name | Configuration | Channels | Price  | Power Supply | Supply Current | Protocols | Package |
	| --------- | ------------- | -------- | ------ | ------------ | -------------- | --------- | ------- |
	|  TMUX646  |   2:1 DPST    |    10    | $0.941 |    3.3, 5    |     0.1 uA     |   MIPI    | NFBGA36 |
	|  TMUX1136 |   2:1 DPST    |    2     | $2.195 |    3.3, 5    |    0.003 uA    |  Analog   | USON-10 |
	|  TMUX121  |   2:1 DPST    |    2     | $0.588 |     3.3      |     11 uA      |  Ana, I2C | UQFN-10 |
	|  TMUX1237 |   2:1 DPST    |    1     | $0.459 |    3.3, 5    |    0.003 uA    |  Analog   |  SOT-6  |
	|  TMUX1575 |   2:1 DPST    |    4     | $0.736 |     3.3      |      7 uA      |  Ana, SPI | DSBGA16 |
=======
>>>>>>> Stashed changes
| Chip Name | Configuration | Channels | Price | Power Supply | Supply Current | Protocols | Package |
| --------- | ------------- | -------- | ----- | ------------ | -------------- | --------- | ------- |
|  TMUX646  |   2:1 DPST    |    10    | $.941 |    3.3, 5    |     0.1 uA     |   MIPI    | NFBGA36 |
|  TMUX1136 |   2:1 DPST    |    2     | ----- |    3.3, 5    | -------------- | --------- | ------- |
|  TMUX121  |   2:1 DPST    |    2     | ----- |     3.3      | -------------- | --------- |  UQFN   |
|  TMUX1237 |   2:1 DPST    |    1     | ----- |    3.3, 5    | -------------- | --------- |  SOT-6  |
|  TMUX1575 |   2:1 DPST    |    4     | ----- |     3.3      | -------------- | --------- | DSBGA16 |
<<<<<<< Updated upstream
=======
>>>>>>> 1c8185f8b94661dedff3b25ba187716a27de10ec
>>>>>>> Stashed changes

The behaviors of the "Mode Selection" switch and the "Default Mode" jumper are both strictly binary. The "Default Mode" jumper shall effectively invert the "Mode Selection" switch output to the MUXes. The "Mode Selection" switch is "active low" (active when grounded) and can be observed as follows:

(1/0 represents active/inactive, not voltage level)
| Default | Mode Sel | Output |
| ------- | -------- | ------ |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

This can be representad as an XOR circuit. If "Mode Selection" and "Default Mode" are both active low, the output of the XOR does not change. This can be achieved by grounding the pins on switch close with a pull up resistor.

-----

Links to component websites:
	
| Chip Name | Website | 
| --------- | ------------- | 
| Selection | https://www.ti.com/switches-multiplexers/analog/products.html#~1143=2%3A1%20SPDT&~3306=3.3%3B5& |
|  TMUX646  | https://www.ti.com/product/TMUX646 |
|  TMUX1136 | https://www.ti.com/product/TMUX1136 |
|  TMUX121  | https://www.ti.com/product/TMUX121 |
|  TMUX1237 | https://www.ti.com/product/TMUX1237 |
|  TMUX1575 | https://www.ti.com/product/TMUX1575 |
