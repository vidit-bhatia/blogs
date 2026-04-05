---
layout: post
title: "How Qubits Are Built: A Tour of Real Quantum Hardware"
date: 2026-02-11 10:00:00 +0000
categories: quantum-computing
tags: [quantum-hardware, superconducting-qubits, trapped-ions, photonic-qubits, neutral-atoms, topological-qubits, physical-qubits]
author: Vidit Bhatia
description: "Explore how qubits are physically built in today's quantum computers. A beginner-friendly tour of superconducting qubits, trapped ions, photonic systems, neutral atoms, and topological approaches."
---

In the [previous post](/blogs/2026/01/25/single-qubit-gates-your-first-quantum-operations/), we learned how to *manipulate* qubits—the mathematical operations that make them do useful work. But there's a question we glossed over: **How do you actually build a qubit in the first place?**

It turns out, there's no single answer. There are at least five different ways researchers and companies are building qubits right now, each with its own physics, advantages, and headaches. In this post, we'll take a high-level tour of the major approaches that are in use or actively developed by the quantum computing industry today.

By the end, you'll understand:

- Why building hardware qubits is so difficult
- The five major physical platforms for qubits
- How each platform works at a basic level
- Why the field hasn't settled on one winner (yet)
- What to expect in deeper posts as we explore each platform in detail

Let's dive in.

## Why Building a Qubit Is Incredibly Hard

Before we see *how* qubits are built, let's talk about *why* it's so challenging.

A qubit is an extremely delicate quantum system. Its quantum state—that precious superposition of 0 and 1—is constantly under attack from the outside world. Any stray heat, electromagnetic noise, vibration, or passing cosmic ray can collapse the superposition into a definite 0 or 1. This phenomenon is called **decoherence**.

Decoherence is the arch-enemy of quantum computing. If a qubit decoheres before you finish your computation, you lose all the quantum advantage. It's like trying to do math on a piece of paper while someone keeps erasing random numbers—you'll never finish the calculation.

So the fundamental challenge in building a qubit is this: **Create a quantum system that is isolated enough to preserve its quantum state, yet controllable enough to apply gates and read out results.**

This is why building qubits requires extreme conditions: ultra-cold temperatures, ultra-high vacuums, precisely engineered electromagnetic fields, or specialized optical systems. Every approach we'll see is trying to solve this same key problem in a different way.

## The Five Major Platforms

Let's tour them.

---

## 1. Superconducting Qubits: The Race Leaders

**The basic idea:** Use an artificial atom made from superconducting electrical circuits.

When you cool certain materials (like aluminum or niobium) below a critical temperature (around 15 millikelvin—nearly absolute zero), they become superconducting: they conduct electricity with zero resistance. Engineers exploit this to create tiny electrical circuits that behave like quantum systems.

A superconducting qubit is typically a small loop of superconducting wire with a crucial weak point: the **Josephson junction**. This junction is an extremely thin insulating barrier (just a few nanometers) sandwiched between two superconducting metals. Here's the magic: even though this insulator is a perfect barrier to normal electrons, in the quantum world, pairs of electrons (called Cooper pairs) can **tunnel through the barrier**—a purely quantum mechanical phenomenon that has no classical equivalent.

### How |0⟩ and |1⟩ Are Encoded

In a superconducting qubit, the quantum states are encoded as **energy levels of the circuit**:

- **|0⟩** = The ground state, or lowest energy level of the superconducting circuit. The Cooper pairs are at rest in their minimum-energy configuration — like a pendulum hanging still, with no oscillation above the baseline. (There is always a tiny irreducible "zero-point energy" from quantum mechanics, but no *extra* energy has been added.)
- **|1⟩** = The first excited state, one energy level higher. A microwave photon has been absorbed, and the Cooper pairs are now oscillating with exactly one extra quantum of energy — the pendulum is swinging.

When you apply a microwave photon (electromagnetic radiation) at precisely the right frequency, it can excite the circuit from |0⟩ to |1⟩, or vice versa. This is similar to how an electron in an atom jumps between energy shells when you shine light at it—except here, the "atom" is an engineered superconducting circuit.

The tunneling behavior of Cooper pairs through the Josephson junction is what makes this quantum system possible. Without the tunnel effect, the circuit would be purely classical. With it, the two states |0⟩ and |1⟩ can coherently interfere with each other, creating superposition.

### Practical Advantages & Challenges

**Why it's popular:**

- Fast gates (nanoseconds) — Microwave pulses can flip a qubit very quickly
- Relatively easy to scale to many qubits — You can etch many junctions on a single chip
- Mature fabrication process (borrowed from classical semiconductor industry) — Similar to how computer chips are made
- Multiple companies are shipping systems: **IBM, Google, Rigetti, and Alibaba**

**The catch:**

- Requires extreme cooling (dilution refrigerators) — The superconducting state only works near absolute zero (15 mK ≈ −273°C)
- Qubits decohere relatively quickly (microseconds to milliseconds) — Thermal noise and electromagnetic radiation cause the quantum state to collapse
- Susceptible to noise from the environment — Any vibration, stray magnetic field, or heat can disturb the tunneling Cooper pairs

**The Decoherence Problem:** At higher temperatures, thermal vibrations give Cooper pairs enough energy to bypass the Josephson junction without quantum tunneling, turning the quantum system into a classical one. This is why extreme cooling is mandatory.

**In the industry:** IBM's quantum roadmap focuses on superconducting qubits, with their latest systems (e.g., Falcon, Heron) scaling to hundreds of qubits. Google's Sycamore processor, which achieved quantum supremacy claims in 2019, was built on superconducting qubits. Rigetti Computing and Alibaba also operate superconducting qubit systems accessible to researchers.

*Sources: Ko et al. (2023) provide an overview of superconducting qubit engineering; IBM's Quantum roadmap documents are publicly available [https://www.ibm.com/quantum](https://www.ibm.com/quantum). Google's 2019 supremacy work appeared in Nature.*

---

## 2. Trapped Ions: The Precision Specialists

**The basic idea:** Trap a single ionized atom using electromagnetic fields, then use laser pulses to manipulate it.

Take a single atom (often ytterbium, calcium, or barium), strip away an electron to ionize it, and suspend it in space using electric and magnetic fields. The trapped ion sits in a region where electromagnetic forces (from carefully shaped electric potential) push it back toward the center—like a 3D trap. Picture a ball rolling in a smooth valley; it naturally returns to the bottom.

### How |0⟩ and |1⟩ Are Encoded

In trapped-ion systems, the quantum states are encoded as **internal energy levels of the atom**:

- **|0⟩** = The atom is in its ground state, a low-energy electronic configuration. For example, an electron in the outermost shell is in a specific orbital.
- **|1⟩** = The atom is in an excited state, with the electron promoted to a higher-energy orbital. This is like the electron has absorbed energy and jumped to a higher shell.

A **laser pulse** tuned to a specific frequency (color) excites the atom from |0⟩ to |1⟩. The laser frequency must match the energy difference between the two states (this is called resonance). When the laser is turned on briefly, it imparts energy; when it's turned off, the atom stays in |1⟩ (until you hit it with another laser pulse).

### Why This Is Quantum, Not Just Two Switches

The resonance condition above might sound like any classical two-level system—a light switch that flips between on and off. So what makes a trapped ion genuinely quantum?

**1. Discrete energy levels (quantization)**
Unlike a classical oscillator that can absorb any amount of energy continuously, the atom's electron levels are quantized. Only a photon with *exactly* the right energy ($E = h\nu$) can drive the transition. This isn't just careful tuning—it is a fundamental consequence of quantum mechanics. The energy levels are discrete by nature, not by engineering.

**2. Superposition**
Between flipping from |0⟩ to |1⟩, the atom can exist in a coherent mix of both states simultaneously. A precisely timed "half-pulse" (called a $\pi/2$ pulse) leaves the atom in the state:

$$\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$$

This is not "halfway between 0 and 1" in any classical sense—it is genuinely both at once, until measured. A classical two-level switch has no equivalent. There is no position on a light switch that means "both on and off."

**3. Phase coherence**
A quantum state carries a *phase*—think of a spinning arrow on a clock face rather than just a position. The phase of the laser pulse directly sets and controls the qubit's phase. Quantum algorithms exploit interference between these phases, amplifying correct answers and canceling wrong ones. Classical bits carry no such phase.

**4. Entanglement via phonons**
When two trapped ions are coupled through their shared vibrational modes (phonons), measuring one ion's state instantaneously constrains what you will find when you measure the other—no matter how far apart they are. This is entanglement: a strictly quantum correlation with no classical equivalent.

The table below captures the contrast:

| Property | Classical two-level system | Trapped-ion qubit |
|---|---|---|
| States | Only 0 or 1 | Any $\alpha\|0\rangle + \beta\|1\rangle$ |
| Energy absorption | Continuous range | Only exact resonant frequency |
| Phase | Irrelevant | Physical and controllable |
| Two-system correlations | Local | Can be entangled (non-local) |

The resonance condition is the *gateway* into this quantum behavior—it ensures a single photon couples to a single energy transition. But the real quantum magic begins once the atom is in superposition between those two levels.

Because the ion is **perfectly isolated** in the trap (no other atoms nearby to collide with), the electronic states remain coherent for remarkably long times—seconds to minutes. This is why trapped ions are so precise: there's minimal environmental disturbance.

Multiple trapped ions interact through their shared motion (phonons—vibrations of the ions)—this is the key to creating entanglement between qubits, which is essential for multi-qubit gates.

### Practical Advantages & Challenges

**Why it's promising:**

- Extraordinary precision and coherence times (seconds to minutes) — The isolated electronic states barely interact with the environment
- All qubits are identical (perfect reproducibility) — Every ytterbium atom is the same; no variability from device to device
- Gates operate with very high fidelity — Laser control is extremely precise
- Measurement readout is nearly perfect — Detecting whether an atom is in |0⟩ or |1⟩ via fluorescence is very reliable

**The catch:**

- Gates are slower (microseconds to milliseconds) — Laser pulses take time to manipulate the electron states
- Harder to scale: trapping and laser-controlling 1,000 qubits is much harder than managing 1,000 superconducting qubits — Each ion needs precise alignment of magnetic and electric fields, and you need dedicated lasers for each one
- Requires specialized high-power lasers and vacuum systems — The ions must be isolated in an ultra-high vacuum to prevent collisions

**In the industry:** **IonQ** and **Honeywell-Quantinuum** (following a 2021 merger) are the leaders. IonQ has announced systems with 11–16 qubits and reported high-fidelity operations. Honeywell/Quantinuum is targeting systems with dozens to hundreds of qubits. Both companies offer cloud access to their systems.

*Sources: Bruzewicz et al. (2019) in Applied Physics Reviews provides a comprehensive review of trapped-ion qubits. IonQ's technical papers and Honeywell/Quantinuum's announcements are available on their websites.*

---

## 3. Photonic Systems: Light as Qubits

**The basic idea:** Use photons (particles of light) as qubits, and manipulate them with optical components.

Instead of storing quantum information in a superconducting circuit or an atom, photonic quantum computers encode it in light itself. A single photon (or a property of it) encodes quantum information. You then use optical components—beam splitters, phase shifters, mirrors, and detectors—to manipulate and measure the qubits.

### How |0⟩ and |1⟩ Are Encoded

Photonic systems use two main approaches:

**Approach 1: Polarization Encoding**
- **|0⟩** = Horizontal polarization (the photon's electric field oscillates left-right)
- **|1⟩** = Vertical polarization (the photon's electric field oscillates up-down)

A **polarizing beam splitter** can distinguish between these two states, separating horizontal photons from vertical ones. A **half-wave plate** (a piece of optical material) can rotate the polarization, effectively applying quantum gates.

**Approach 2: Continuous-Variable (Amplitude & Phase) Encoding**
- Information is encoded in the amplitude and phase of the light wave itself, rather than single photons. This is what **Xanadu** uses: they squeeze light (reduce noise in one direction at the expense of the other) to create quantum advantage. The states |0⟩ and |1⟩ correspond to different combinations of amplitude and phase.

**Why it works:** Photons are exceptionally well-isolated from thermal noise (light doesn't care about temperature), and optical components are proven technology from telecommunications. **Beam splitters** guide photons along different paths; **phase shifters** change the quantum phase; **detectors** measure the final state.

### Why This Is Quantum, Not Just Classical Optics

Light and lenses have been around for centuries. So what makes a photonic quantum computer quantum rather than just a very fancy optical bench?

**1. The photon is a single quantum of light**
Classical optics works with continuous beams of light—millions or billions of photons at once. Photonic quantum computing works with *individual* photons, each carrying exactly one quantum of energy ($E = h\nu$). You cannot have half a photon. The indivisibility of the photon is a purely quantum property; there is no classical analogue for a single, discrete packet of light.

**2. A single photon can be in superposition**
When a single photon hits a 50/50 beam splitter, it does not "choose" to go left or right. Quantum mechanically, it travels *both paths simultaneously*, in the state:

$$\frac{1}{\sqrt{2}}(|\text{left}\rangle + |\text{right}\rangle)$$

This is not a probabilistic coin flip decided in advance—it is a genuine quantum superposition. The two paths interfere with each other, and you can prove this by recombining them: the photon always exits from one specific port when the path lengths are equal (constructive interference), and never from the other (destructive interference). A classical ball bearing going through a physical beam splitter shows no such interference.

**3. Polarization states carry quantum phase**
In polarization encoding, the qubit is not simply "horizontal or vertical." It can be in any superposition:

$$\alpha|\leftrightarrow\rangle + \beta|\updownarrow\rangle$$

where $\alpha$ and $\beta$ are complex numbers whose *phases* matter. A half-wave plate rotates this state on the Bloch sphere—not by flipping a switch, but by continuously rotating the quantum amplitude through any angle. Classical polarization filters can only block or pass; they cannot create or rotate a quantum superposition.

**4. Two-photon entanglement**
When two photons are produced together (e.g., via spontaneous parametric down-conversion—a nonlinear crystal that splits one high-energy photon into two lower-energy ones), their polarizations become entangled. Measuring the polarization of one photon instantly determines a correlated outcome for the other, regardless of the distance between them. This is entanglement: a strictly non-classical correlation that has no equivalent in any classical wave or particle picture.

**5. The measurement is irreversible and quantum**
When a single-photon detector fires, that photon is absorbed and destroyed. The quantum state collapses to a definite outcome. This is not like a classical sensor reading an analog value—it is a fundamental quantum measurement event. Before detection, the photon's state was a superposition; after detection, it is one definite outcome, and the original superposition cannot be recovered (this is the no-cloning theorem in action).

| Property | Classical optics (laser beam) | Photonic qubit |
|---|---|---|
| Light quantity | Continuous, many photons | Single, indivisible photon |
| Beam splitter behavior | Splits intensity | Creates quantum superposition |
| Polarization | Continuous amplitude | Discrete quantum state with phase |
| Two-beam correlations | Classical intensity correlations | Can be entangled (non-local) |
| Measurement | Non-destructive, readable | Irreversible, collapses quantum state |

The optical components—beam splitters, wave plates, phase shifters—are classical in construction, but when you send a *single photon* through them, they become quantum gates. The quantum magic lives in the photon itself; the optics just guide it.

**One crucial advantage:** Photons don't need to be cooled to near absolute zero. They're naturally immune to thermal fluctuations.

### Practical Advantages & Challenges

**Why it's compelling:**

- Room-temperature operation (no need for extreme cooling) — Your lab doesn't need a dilution refrigerator
- Natural compatibility with fiber optic networks — Photons can travel through fiber to reach distant qubits
- Potentially easier to scale using optical integrated circuits — Beam splitters and phase shifters can be etched onto photonic chips, similar to electronic chips

**The catch:**

- Photon loss (photons disappear or miss detectors) — A single lost photon is a lost qubit; loss rates of even 1% add up quickly in large circuits
- Weak photon-photon interactions (hard to create two-qubit gates) — Photons barely interact with each other naturally; creating two-qubit gates requires clever tricks (like using nonlinear optical materials) or additional resources
- Currently fewer qubits than superconducting or trapped-ion systems — Scaling the number of qubits requires managing many independent photons and detectors reliably

**In the industry:** **Xanadu** (based in Toronto) is the leading developer of photonic quantum computers, using squeezed light and Gaussian operations. **PsiQuantum**, another photonic approach, is also advancing the field. Both are pursuing different architectural strategies.

*Sources: Braunstein & van Loock (2005) in Reviews of Modern Physics cover continuous-variable photonic systems; Xanadu's papers on their approach are accessible via [https://www.xanadu.ai](https://www.xanadu.ai).*

---

## 4. Neutral Atoms: The New Contenders

**The basic idea:** Trap neutral atoms (without removing electrons) using optical tweezers, and control them with laser pulses.

This approach is newer but gaining momentum fast. A neutral atom is held in place by an **optical tweezer**—a highly focused laser beam that creates a microscopic trap. The laser light interacts with the atom's electrons, pulling the atom toward the brightest part of the beam (like a tiny ball caught in a light beam). When you arrange multiple optical tweezers in a grid, you can trap dozens or hundreds of atoms simultaneously.

### How |0⟩ and |1⟩ Are Encoded

Neutral atoms can be encoded using two main approaches:

**Approach 1: Rydberg Blockade Encoding**
- **|0⟩** = Ground state (the atom's electrons are in their lowest-energy configuration)
- **|1⟩** = Rydberg state (the atom's outermost electron is excited to a very high energy level, far from the nucleus)

A **Rydberg state** is special: the electron is extremely far from the nucleus, making it huge compared to a normal atom—about 100 times larger. This size means Rydberg atoms **strongly interact with each other** even when separated (unlike ground-state atoms). When one atom is in the Rydberg state, it creates an electromagnetic field that prevents neighboring atoms from also entering the Rydberg state—this is called the **Rydberg blockade**, and it's the secret to creating two-qubit gates.

Laser pulses tuned to the right frequency excite the atom from ground state (|0⟩) to Rydberg state (|1⟩). Another laser pulse brings it back down.

**Approach 2: Clock States**
- Some systems encode |0⟩ and |1⟩ as two specific ground-state levels of the atom that are almost identical in energy. Laser pulses transition between them.

**Why this works:** Optical tweezers are extremely reconfigurable—you can create, destroy, or move atoms to different trap sites on microsecond timescales. This flexibility is a huge advantage over fixed superconducting circuits.

### Why This Is Quantum, Not Just Atoms in Laser Traps

Optical tweezers by themselves are not enough to make a quantum computer. They are excellent positioning tools. The quantum part appears when the atom's internal states are controlled coherently and made to interact through Rydberg physics.

**1. Quantized atomic levels**
Each neutral atom has discrete energy levels. A control laser can drive transitions only when its frequency matches the exact level spacing. This resonance condition is quantum mechanical, not classical tuning.

**2. Coherent superposition of internal states**
With a carefully timed pulse (for example, a $\pi/2$ pulse), the atom can be prepared in:

$$\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$$

This means the atom is in a coherent combination of both basis states until measurement. A classical trapped particle can be in one state or another, but not in a phase-coherent blend of both.

**3. Rydberg blockade creates controllable interaction**
When one atom is excited to a Rydberg state, it shifts neighboring atoms' energy levels so strongly that nearby atoms cannot be excited at the same time. This "you go first, I must wait" effect is the Rydberg blockade, and it is the engine behind two-qubit entangling gates.

**4. Entanglement from shared blockade dynamics**
Applying the right pulse sequence to two atoms inside a blockade radius can create an entangled state such as:

$$\frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)$$

Now the two atoms no longer have independent states; the system must be described as one joint quantum state.

**5. Measurement collapses the quantum state**
Readout is typically done by state-dependent fluorescence: one state scatters light strongly while the other appears dark. Before measurement, the atom may be in superposition; after detection, the outcome is definite. This collapse behavior is a core quantum feature.

| Property | Classical atom trap | Neutral-atom qubit platform |
|---|---|---|
| Atom position | Localized particle in a trap | Localized particle + controlled internal quantum state |
| State control | Classical motion control | Coherent control of $|0\rangle$ and $|1\rangle$ |
| Multi-atom coupling | Weak, mostly independent | Strong Rydberg-mediated interaction |
| Correlations | Classical | Entanglement possible |
| Measurement | Position/intensity readout | Quantum projective readout |

So the tweezers provide the hardware scaffold, but the quantum computer emerges from coherent state control, phase-preserving evolution, and entangling Rydberg interactions.

### Practical Advantages & Challenges

**Why it's generating excitement:**

- Potentially easier to scale to 1,000+ qubits (you can move atoms around via tweezers and reconfigure the trap geometry dynamically)
- Fast gates (microseconds) — Rydberg interactions happen quickly
- Fewer specialized cooling requirements than trapped ions — No need for ultra-high vacuum; atoms can tolerate some background gas
- Qubits can be created flexibly (add or remove atoms as needed) — Want to remove a bad qubit mid-computation? Just switch off that tweezer

**The catch:**

- Very new technology; less maturity than superconducting or trapped-ion systems — Still working out scalability and practical issues
- Atom loss (atoms can escape the trap) — Optical traps are not 100% stable; atoms occasionally heat up and escape
- Coherence times are moderate (milliseconds) — Shorter than trapped ions but longer than superconducting qubits
- Complex laser systems — You need high-power lasers to create and manipulate the tweezers

**In the industry:** **QuEra Computing** (founded by MIT researchers) and **Atom Computing** are the leading companies. Atom Computing announced a 1,000-qubit neutral atom system in 2023 (though practical utility is still being developed). Multiple university groups (e.g., at UC Berkeley, MIT, University of Wisconsin) are also advancing the technology.

*Sources: Endres et al. (2016) in Science demonstrated the Rydberg approach; Atom Computing and QuEra's technical announcements and papers are available on their websites.*

---

## 5. Topological Qubits: The Long-Term Bet

**The basic idea:** A qubit encoded in a topological property of a physical system that is inherently protected from noise by the laws of topology itself.

This is the most speculative approach on our list, but it's backed by serious research and investment.

Topological quantum computing relies on exotic quantum phenomena, called "topological protected states," that are resistant to decoherence by their very nature. The most famous candidate is the **Majorana fermion**—a particle (or qubit) that exists at the edge of certain materials, and whose quantum information is encoded in a way that is "topologically protected."

### How |0⟩ and |1⟩ Are Encoded (Theory)

The exact encoding depends on the approach, but the main idea is:

- **|0⟩ and |1⟩** are encoded in the *topological properties* of a condensed-matter system (e.g., a superconductor with special magnetic properties). The information is not stored in a single location but distributed across the system in a way that is robust against local perturbations.

Think of it like this: In normal qubits, if a stray photon hits your superconducting circuit, it can flip |0⟩ to |1⟩ (an error). But in a topological qubit, the |0⟩ and |1⟩ states are so fundamentally different *in a global, topological sense* that a single local perturbation cannot flip between them. You'd need a massive, coordinated change to the entire system to cause an error.

**The catch:** This is still mostly theoretical. Majorana fermions have not yet been conclusively demonstrated, and engineering a practical topological quantum computer is a grand challenge.

### Practical Advantages & Challenges (Theoretical)

**Why it's worth pursuing:**

- Inherent protection against errors (potentially error-free qubits) — Errors would require breaking topological symmetry, which is exponentially hard
- Could dramatically reduce the need for error correction — Today's quantum computers spend most of their resources correcting errors; topological qubits could change that
- If it works, it changes the game — The quantum computing landscape would be transformed

**The catch:**

- Fundamental physics still being explored — We don't yet have definitive proof that Majorana fermions exist as qubits
- No large-scale system yet; early proof-of-concept stage — We're still in the "does this even work?" phase, not the "how do we scale it?" phase
- Unclear whether Majorana fermions or other topological systems can be engineered at scale — Creating and manipulating topological states reliably remains an open problem
- Still requires extreme cooling — Most topological platforms still need near-absolute-zero temperatures

**In the industry:** **Microsoft** is the main backer, funding significant research into topological qubits. They haven't yet shipped a full topological system, but they've demonstrated key physics milestones.

*Sources: Nayak et al. (2008) in Reviews of Modern Physics is a seminal review of topological quantum computing. Microsoft's announcements and collaborations with academia are publicly available.*

---

## Honorable Mentions

Two other approaches deserve a brief nod:

**NMR (Nuclear Magnetic Resonance) Qubits:** Used early quantum computers and are still valuable for research, but don't scale well to large numbers of qubits. They're not pursued for commercial systems today.

**Quantum Dots:** Electrons or holes trapped in tiny semiconductor structures. CapitalQ and others are exploring this, but it's still in research phases, with coherence and control challenges.

---

## Why So Many Approaches?

You might wonder: with all these platforms, why hasn't one clearly "won"?

The answer is that **the quantum computing hardware problem is genuinely hard**, and no single platform has yet checked all the boxes:

- **Superconducting**: Fast and scalable, but short coherence times
- **Trapped ions**: Exquisite precision, but slower and harder to scale
- **Photonic**: Room temperature, but hard to make photons interact
- **Neutral atoms**: Promising scaling, but still early stages
- **Topological**: Ultimate robustness, but fundamental physics still uncertain

The industry is pursuing all five approaches simultaneously because:

1. Each has different bottlenecks (errors, coherence, speed, scalability)
2. Different applications may favor different platforms
3. We're still in an exploratory phase; it's too early to bet everything on one horse
4. Competition drives innovation

Over the coming decade, one or more of these will likely emerge as dominant for certain tasks, while others find niche applications. Or we might see hybrid systems combining the best parts of each.

---

## What's Next?

This post has given you a 10,000-foot view of how qubits are built. In the next series of posts, we'll **go deep**, one platform at a time:

1. **Deep dive into Superconducting Qubits**: How exactly do you make a superconducting circuit act like a qubit? What's the Josephson junction? Why do they need such cold temperatures?

2. **Deep dive into Trapped Ions**: How do you trap an atom? What makes ions better at gates than superconductors? How does laser control work?

3. **Deep dive into Photonic Systems**: How can you encode information in light? What are continuous-variable quantum computing and Gaussian operations?

4. **Deep dive into Neutral Atoms**: What's a Rydberg state, and why is it useful? How do optical tweezers work at scale?

5. **Deep dive into Topological Qubits**: What makes a quantum state "topological"? Why would topological protection solve the error problem?

Each deep dive will include schematics, more detailed physics, and real experimental results from leading labs.

---

## Wrap-up

Building a qubit is an engineering and physics challenge unlike most others. You need a quantum system that is **isolated from noise** (for coherence) yet **precisely controllable** (for gates) and **scalable** (for a useful computer). Five major approaches—superconducting, trapped ions, photonic, neutral atoms, and topological—are vying to solve this problem in different ways.

No single winner has emerged, and that's a sign of how hard the problem is. But it's also exciting: the diversity of approaches means that if one hits a fundamental wall, the others may succeed.

---

## Further Reading & Sources

### General Reviews & Overviews
- **Devoret & Schoelkopf (2013)**: "Superconducting Circuits for Quantum Information." *Reviews of Modern Physics*, 85(3), 1169.
  - Comprehensive technical review of superconducting qubits. [https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.85.1169](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.85.1169)

- **Bruzewicz et al. (2019)**: "Quantum Computing with Trapped Ions." *Applied Physics Reviews*, 6, 021314.
  - Detailed review of trapped-ion systems. [https://aip.scitation.org/doi/10.1063/1.5088164](https://aip.scitation.org/doi/10.1063/1.5088164)

- **Nayak et al. (2008)**: "Non-Abelian Anyons and Topological Quantum Computation." *Reviews of Modern Physics*, 80(3), 1083.
  - Seminal review on topological quantum computing. [https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.80.1083](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.80.1083)

### Superconducting Qubits
- **Ko et al. (2023)**: "Superconducting Qubits and the Physics of Josephson Junctions." *Nature Reviews Physics*, 5, 45–67.
  - Recent overview of superconducting device physics.

- **IBM Quantum** — [https://www.ibm.com/quantum](https://www.ibm.com/quantum)
  - IBM's quantum roadmap, educational resources, and access to superconducting qubit systems.

- **Google Quantum AI** — [https://quantumai.google/](https://quantumai.google/)
  - Google's quantum research and demonstrations (including the 2019 quantum supremacy paper in Nature).

### Trapped Ions
- **IonQ** — [https://www.ionq.com/](https://www.ionq.com/)
  - Technical papers, system specifications, and cloud access.

- **Honeywell Quantinuum** — [https://www.quantinuum.com/](https://www.quantinuum.com/)
  - Joint venture combining Honeywell's quantum division with Cambridge's Quantinuum; Technical announcements and research.

### Photonic Quantum Computing
- **Braunstein & van Loock (2005)**: "Quantum Information with Continuous Variables." *Reviews of Modern Physics*, 77(2), 513.
  - Foundation for understanding continuous-variable photonic systems. [https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.77.513](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.77.513)

- **Xanadu** — [https://www.xanadu.ai/](https://www.xanadu.ai/)
  - Xanadu's photonic quantum computing approach and papers.

- **PsiQuantum** — [https://psiquantum.com/](https://psiquantum.com/)
  - PsiQuantum's fault-tolerant photonic architecture.

### Neutral Atoms
- **Endres et al. (2016)**: "Atom-by-atom assembly of defect-free one-dimensional cold atom arrays." *Science*, 354(6315), 1024–1027.
  - Landmark paper on optical tweezer trapping. [https://science.sciencemag.org/content/354/6315/1024](https://science.sciencemag.org/content/354/6315/1024)

- **Atom Computing** — [https://www.atom-computing.com/](https://www.atom-computing.com/)
  - Their 1,000-qubit neutral atom announcement and technical details.

- **QuEra Computing** — [https://www.quera.com/](https://www.quera.com/)
  - QuEra's Rydberg-atom approach and research papers.

### Topological Qubits
- **Microsoft Quantum** — [https://www.microsoft.com/en-us/quantum](https://www.microsoft.com/en-us/quantum)
  - Microsoft's topological qubit research, announcements, and collaborations.

### Quantum Hardware Comparison
- **Quantinuum & Honeywell Whitepaper**: "A Blueprint for Quantum Computing" — Overview of different platforms and their trade-offs.

---

## Previous Post
[Single-Qubit Gates: Your First Quantum Operations](/blogs/2026/01/25/single-qubit-gates-your-first-quantum-operations/)

## Next in the Series
*Deep Dive: Superconducting Qubits—From Josephson Junctions to Quantum Supremacy* (Coming soon)
