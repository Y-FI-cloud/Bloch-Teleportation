# ⚛️ Quantum Teleportation Simulator

A Python simulation of the **quantum teleportation protocol** using [Qiskit](https://qiskit.org/), complete with Bloch sphere visualization, ideal vs. noisy simulation comparison, and a bar chart analysis of measurement outcomes.

---

## 📌 What It Does

This script simulates the full quantum teleportation protocol, where an arbitrary qubit state is transferred from Alice to Bob using:
- A **pre-shared Bell pair** (entanglement)
- A **Bell measurement** on Alice's side
- **Classical corrections** applied on Bob's qubit

The simulation runs twice — once under **ideal conditions** and once with a **depolarizing noise model** — so you can directly compare how real-world noise affects the fidelity of teleportation.

---

## 🔬 Protocol Overview

```
Alice's qubit (|ψ⟩) ──[RY(θ)]──●──[H]──M ────────────────────────
                                 │               ↓ (classical bits)
Bell pair qubit 1   ────[H]──●──X──────M ──────────────────────────
                              │               ↓
Bell pair qubit 2   ──────────X────────────[CX]──[CZ]── Bob's qubit
```

1. Alice prepares a qubit in state `|ψ⟩ = RY(θ)|0⟩`
2. A Bell pair is created between qubits 1 and 2
3. Alice performs a Bell measurement on her two qubits
4. Bob applies conditional `X` and `Z` corrections based on Alice's classical results
5. Bob's qubit is now in state `|ψ⟩`

---

## 📊 Outputs

- **Bloch sphere visualization** of all three qubit states before measurement
- **Console table** comparing ideal vs. noisy measurement distributions across all 8 basis states
- **Bob's qubit marginal** — how often Bob receives `|0⟩` vs `|1⟩`
- **Bar chart** comparing ideal and noisy simulation probabilities side by side

---

## 🛠️ Requirements

- Python 3.8+
- [Qiskit](https://pypi.org/project/qiskit/) (`qiskit`)
- [Qiskit Aer](https://pypi.org/project/qiskit-aer/) (`qiskit-aer`)
- NumPy
- Matplotlib

Install all dependencies with:

```bash
pip install qiskit qiskit-aer numpy matplotlib
```

---

## 🚀 Usage

```bash
python Bloch_Teleportation.py
```

You can tune the simulation parameters at the top of the file:

| Parameter   | Default     | Description                                      |
|-------------|-------------|--------------------------------------------------|
| `theta`     | `π/4`       | Rotation angle defining the qubit state to teleport |
| `p_error`   | `0.05`      | Depolarizing error probability (5%)              |
| `num_shots` | `1000`      | Number of measurement shots per simulation       |

---

## 🧪 Example Output

```
--- DETAILED STATE COMPARISON ---
State        | Ideal (%)    | With 5% Noise (%)
----------------------------------------------
   000       |    85.3%     |      71.2%
   001       |     0.0%     |       4.1%
   ...

--- BOB'S RECEIVED MESSAGE (Qubit 2) ---
Measurement  | Ideal (%)    | With 5% Noise (%)
----------------------------------------------
Received '0' |    85.3%     |      68.7%
Received '1' |    14.7%     |      31.3%
```
<img width="1791" height="602" alt="image" src="https://github.com/user-attachments/assets/92988b9e-c52a-48cb-bd2e-de4a768c1889" />

<img width="996" height="490" alt="image" src="https://github.com/user-attachments/assets/a0131256-9f2e-45e9-887c-9d82a4248761" />


     ┌─────────┐ ░            ░      ┌───┐ ░          ░ ┌─┐      
q_0: ┤ Ry(π/4) ├─░────────────░───■──┤ H ├─░───────■──░─┤M├──────
     └─────────┘ ░ ┌───┐      ░ ┌─┴─┐└───┘ ░       │  ░ └╥┘┌─┐   
q_1: ────────────░─┤ H ├──■───░─┤ X ├──────░───■───┼──░──╫─┤M├───
                 ░ └───┘┌─┴─┐ ░ └───┘      ░ ┌─┴─┐ │  ░  ║ └╥┘┌─┐
q_2: ────────────░──────┤ X ├─░────────────░─┤ X ├─■──░──╫──╫─┤M├
                 ░      └───┘ ░            ░ └───┘    ░  ║  ║ └╥┘
c: 3/════════════════════════════════════════════════════╩══╩══╩═
                                                         0  1  2 

---

## 📚 Background

Quantum teleportation was first proposed by Bennett et al. in 1993. It does **not** transfer matter or allow faster-than-light communication — the classical correction step ensures that. What it does transfer is the complete quantum state of a qubit, which cannot be copied (no-cloning theorem) but can be moved through this protocol.

---

## 📄 License

MIT License — feel free to use, modify, and share.
