# Selfish Mining: Simulation and Learning-Automata Defense

A Python simulator for **selfish mining** attacks on Bitcoin, and for a defense mechanism based on
learning automata.

**Original author:** Ali Nikhalat-Jahromi. This repository is a fork of
[AliNikhalat/SelfishMining](https://github.com/AliNikhalat/SelfishMining). The work was carried out
jointly by Ali Nikhalat-Jahromi, Ali Mohammad Saghiri, and Mohammad Reza Meybodi.

## Background

In selfish mining, a miner with a large share of the computing power keeps newly found blocks private
and releases them strategically, earning more than its fair share of rewards. The defense studied here
changes how honest miners resolve forks, and uses learning automata to adapt its parameters to the
network.

## Publications

- A. Nikhalat-Jahromi, A. M. Saghiri, M. R. Meybodi, "Nik Defense: An Artificial Intelligence Based
  Defense Mechanism against Selfish Mining in Bitcoin," [arXiv:2301.11463](https://arxiv.org/abs/2301.11463).
- A. Nikhalat-Jahromi, A. M. Saghiri, M. R. Meybodi, "VDHLA: Variable Depth Hybrid Learning Automaton
  and Its Application to Defense Against the Selfish Mining Attack in Bitcoin,"
  [arXiv:2302.12096](https://arxiv.org/abs/2302.12096).
- A. Nikhalat-Jahromi, A. M. Saghiri, M. R. Meybodi, "Asymmetric Variable Depth Learning Automaton and
  Its Application in Defending Against Selfish Mining Attacks on Bitcoin," *Applied Soft Computing*,
  vol. 170, 2025.

## What is in the repository

| Folder | What it is |
| --- | --- |
| `sm1/` | The original selfish mining strategy of Eyal and Sirer (SM1). |
| `optimal/` | A solver for optimal selfish mining strategies, after Sapirshtein, Sompolinsky, and Zohar. |
| `nik_sm/` | Selfish mining against the Nik defense, with the learning automata that drive it. |
| `nik_sm/learning_automata/` | Variable action-set automaton (VASLA) and the symmetric and asymmetric variable depth hybrid automata (SVDHLA, AVDHLA). |
| `tests/` | Experiment scripts comparing the defense with SM1 and across parameter settings. |

## Run it

Requires Python 3 with NumPy, SciPy, and Matplotlib.

```bash
pip install numpy scipy matplotlib

# Baseline: selfish mining without a defense
cd sm1 && python sm1_main.py

# Selfish mining against the Nik defense
cd nik_sm && python nik_sm_main.py

# Comparison experiments (run from the repository root)
python tests/nik_selfish_mining_sm1_comparison_test.py
```

Each run prints the number of blocks won by honest and selfish miners, the number of stale blocks, and
the revenue share of each side.

## Main parameters

| Parameter | Meaning |
| --- | --- |
| `alpha` | Share of total mining power held by the selfish miner. |
| `gamma` | Fraction of honest miners that mine on the selfish miner's block during a tie. |
| `tow_number`, `min_tow_block_number`, `max_tow_block_number` | Time-window settings of the defense. |
| `LearningAutomataType` | Which automaton adapts the defense: `VASLA`, `SVDHLA`, or `AVDHLA`. |
