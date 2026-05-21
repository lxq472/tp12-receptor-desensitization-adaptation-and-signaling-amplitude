# Receptor Desensitization, Adaptation and Signaling Range Expansion

This project implements theoretical and computational models of:

* receptor desensitization
* biochemical adaptation
* integral negative feedback
* signaling range expansion
* fold-change detection (FCD)

---

# 📌 Overview

Many biological signaling systems respond transiently to sustained stimulation.

Key idea:

> Cells often respond to changes in input rather than absolute ligand concentrations.

This phenomenon is known as:

* adaptation
* receptor desensitization
* fold-change detection

and appears in:

* GPCR signaling
* neutrophil chemotaxis
* insulin signaling
* WNT signaling

---

# 🔹 1. Michaelis-Menten Kinetics

The project begins with the derivation of the classical Michaelis-Menten reaction:

```text
dP/dt = k3 * Et * S / (S + KM)
```

with:

```text
KM = (k2 + k3)/k1
```

using:

* enzyme conservation
* quasi-steady-state approximation (QSSA)

---

# 🔹 2. Feedback Algebra

The signaling networks are linearized around steady state using the Jacobian matrix:

```text
dx/dt = Jx
```

The analysis includes:

* signs of interaction terms
* feedback topology
* determinant conditions for adaptation
* network stability

Key result:

```text
Perfect adaptation ⇔ |N| = 0
```

where `N` is the relevant Jacobian minor.

---

# 🔹 3. Adaptive Signaling Network

## Network Topology

```text
I → A → C
      ↑
      |
      B
```

where:

* `A` = activation node
* `B` = desensitization / feedback node
* `C` = signaling output

---

## Adaptive Model

```text
dA/dt = kI*I - kFA*A

dB/dt =
    kCB*C*(1-B)/((1-B)+K1)
    - kFB*B/(B+K2)

dC/dt = kAC*A - kBC*B*C
```

---

## Biological Interpretation

The node `B` acts as a delayed negative feedback controller.

When the Michaelis-Menten reactions operate in the saturation regime:

```text
(1-B) >> K1
B >> K2
```

the system behaves approximately as an:

> integral negative feedback controller

which generates adaptation.

---

# 🔹 4. Non-Adaptive Control Network

For comparison, a feedforward system without feedback was simulated:

```text
I → A → C
```

with equations:

```text
dA/dt = kI*I - kFA*A

dC/dt = kAC*A - kC*C
```

---

# 🔹 5. Adaptive Transient Response

The adaptive system exhibits:

* rapid activation
* transient pulse response
* gradual return toward baseline

This is the characteristic signature of receptor desensitization.

---


# 🔹 6. Signaling Range Expansion

The response amplitude was quantified as:

```text
(Cmax - C1)/C1
```

across several orders of magnitude of input stimulation.

---

## Comparison

### Adaptive Network

* weak dependence on input magnitude
* broader dynamic range
* reduced saturation
* approximate Weber-like behavior

### Non-Adaptive Network

* strong dependence on absolute input
* loss of sensitivity at high stimulation
* no adaptation

---

# 🔹 7. Key Insight

The adaptive network does not produce perfectly constant responses across all inputs, but it strongly compresses the dependence of signaling on stimulus magnitude.

This occurs because:

* the feedback behaves approximately as an integral controller
* the system operates in the saturation regime
* the output becomes partially insensitive to absolute ligand concentration

These properties are closely related to:

* adaptation
* Weber’s law
* fold-change detection (FCD)

---

# 📊 Simulations

The repository includes simulations of:

* adaptive vs non-adaptive signaling
* transient pulse responses
* signaling range expansion
* nonlinear feedback dynamics

Metrics include:

* output concentration `C(t)`
* transient peak response
* relative response amplitude
* sensitivity across input scales

---

# 📌 Conclusions

* Receptor desensitization expands signaling range
* Integral negative feedback produces adaptation
* Adaptive systems respond primarily to relative changes
* Non-adaptive systems saturate rapidly
* Saturation kinetics are essential for fold-change-like behavior

---

# 📚 References

* Prof. Ala Trusina, NFYK14009U Physics of Molecular Diseases, Niels Bohr Institute, University of Copenhagen

* Ma W. et al. (2009)
Defining Network Topologies that Can Achieve Biochemical Adaptation*  
Cell

* Shoval O. et al. (2010)
Fold-change detection and scalar symmetry of sensory input fields*  
PNAS

* Goentoro L. et al. (2009)
The Incoherent Feedforward Loop Can Provide Fold-Change Detection in Gene Regulation*  
Molecular Cell

---
