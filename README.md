# ⚡ High-Power ZVS Driver

> A Mazzilli-topology Zero-Voltage-Switching driver, simulated, built and characterized on the bench. Built to understand one of the most elegant self-oscillating circuits in power electronics.

![ZVS driver board](images/zvs_board.jpeg)

---

## 🎯 Why this project

The ZVS is a circuit that looks almost too simple for what it does: two MOSFETs, a handful of passives, no controller, no microcontroller — and it self-oscillates at exactly the right frequency, switching each transistor at the precise moment its drain voltage crosses zero.

I built it to understand *why* that works. Along the way it also became a working induction heater.

---

## 📐 Specifications

| | |
|---|---|
| **Topology** | Mazzilli ZVS (self-oscillating push-pull) |
| **Switching devices** | 2 × IRFP260N |
| **Rated current** | Up to 18 A |
| **Tested up to** | 8 A |
| **Tank capacitors** | 2 × 0.33 µF double-metallized film, 9.8 A each |
| **Choke** | 100 µH |
| **Input filtering** | 100 µF / 50 V |
| **Gate network** | 470 Ω / 2 W feed resistors, 10 kΩ pulldowns, 12 V zeners, UF4007 clamp diodes |

**On operating frequency:** a ZVS has no fixed switching frequency — it's set by the resonant tank, so it depends entirely on the inductance and impedance of whatever work coil is attached. Change the coil, change the frequency. That's the whole point of the topology.

---

## 🔬 From simulation to hardware

The first step of this project wasn't a soldering iron — it was **LTspice**. Before touching a single component I simulated the full circuit to understand the oscillation mechanism and verify the passive values.

![LTspice simulation](images/ltspice_sim.png)

The simulation files are in [`/simulations`](simulations/).

Then came a **breadboard prototype**, and finally the custom PCB.

![Breadboard prototype](images/breadboard_proto.jpeg)

---

## 🖥️ PCB

![PCB layout](images/pcb_layout.png)

---

## 📊 Bench characterization

The defining claim of a ZVS is in its name: each MOSFET switches when the voltage across it is at zero, which is why the losses stay so low. So that's what I went looking for on the scope — and confirmed. **Switching happens at the zero crossing**, as designed.

![Scope capture](images/scope_zvs.jpeg)

Everything was verified with a work coil attached, running the tank at resonance.

**Thermal behaviour:** at just under 10 A, nothing on the board runs hot — not the MOSFETs, not the resistors, not the caps. The components are comfortably sized for the job.

---

## 🔥 Induction heating

With a work coil on the output, the driver becomes an induction heater.

*(photos coming)*

---

## ⚠️ Safety

This circuit handles serious power. Even at the currents shown here, the tank voltage across the coil is far higher than the supply voltage, and the components store enough energy to be genuinely dangerous.

I'm interested in eventually driving high-voltage transformers with it — but only with proper equipment and proper supervision. **Don't reproduce this unless you know exactly what you're doing.**

---

## 📚 References

Built after working through the classic technical documentation on the topology, along with explainer videos from **ElectroBOOM** and others in the community who've covered this circuit well.

---

## 🛠️ Built with

`LTspice` · `KiCad` · `Oscilloscope characterization` · `Power electronics`
