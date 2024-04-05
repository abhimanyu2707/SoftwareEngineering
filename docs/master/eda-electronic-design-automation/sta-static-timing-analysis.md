# STA(Static Timing Analysis)

### What does it do

* Used to validate the timing performance of a design by checking all possible paths for timing violation.
* Breaks design into timing paths.
* Calculate signal propagation delays along each path.
* Timing constraints are within the design and at the input/output interface.
* It's a violation if constraints are not met.

### Compared with dynamic simulation

* It does not simulate the logical operation of the design and is faster because of this.
* It is also more thorough than dynamic simulation as it checks all paths, not just a set of test vectors which are used for logical checks in simulation.

### How does it work

* Breaks the design into timing paths, which contain:
  * **Startpoint:** input port or a register clock pin(from where the data is launched by a clock edge).
  * **Combinational Logic network: Elements with no memory or internal state.** e.g. AND, OR, XOR, Invert, etc.
  * **Endpoint:** output port or a register data input pin.
* Combinational logic may contain multiple paths. The longest path is taken for maximum delay calculation and the shortest for minimum delay calculation.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>From Synopsis website</p></figcaption></figure>

There are other paths:

* **Clock path:** From a clock input port to the clock pin of a sequential element. For setup and hold check.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>From Synopsis website</p></figcaption></figure>

* After breaking down the design into a set of timing paths, the delays along each path are calculated.
  * cell delay + net dealy
  * **cell delay:** From the SDF file, if not then from the delay table in the logic library file.
  * **net delay:** Function of capacitance, resistance, and drive strength of cell driving the net.
* Two types of timing constraints are checked for violation:
  * **Setup violation:** If new data is not available in a stable state before the clock reaches. This constraint enforces a maximum delay on the data path relative to the clock edge.
  * **Hold violation:** If new data reaches and the previous clock is still reading or is in an unstable state. This constraint enforces a minimum delay on the data path relative to the clock edge.
* By default, the tool assumes that the signals are propagated through each data path in one clock cycle. But there are some exceptions.
  * **False path:** No need for analysis.
  * **Multicycle path:** Data path taking more than one cycle from launch to capture.
  * **Minimum and Maximum delay constraint** on a path.
