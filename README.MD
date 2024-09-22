# Schrodinger Neural Network

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Theoretical Explanation](#theoretical-explanation)

## Introduction

This project demonstrates how to approximate the solutions of the time-independent Schrödinger equation for a quantum particle in a one-dimensional harmonic oscillator potential using neural networks. By leveraging PyTorch, the project employs neural networks to estimate the ground state and excited state wavefunctions without relying on traditional numerical methods.

## Features

- **Ground State Solution:** Approximates the lowest energy state of the harmonic oscillator.
- **First and Second Excited States:** Extends the model to compute higher energy states while enforcing orthogonality constraints.
- **Visualization:** Compares neural network solutions with exact analytical solutions through detailed plots.

## Technologies Used

- **Python 3.x**
- **PyTorch:** For building and training neural networks.
- **NumPy:** For numerical operations.
- **Matplotlib:** For data visualization.
- **Jupyter Notebook:** For interactive development and demonstration.

## Theoretical Explanation

Quantum mechanics fundamentally describes the behavior of particles at microscopic scales. The main equation for the quantum processes is the **Schrödinger equation**. It is a linear partial differential equation. Fundamentally, it is a time dependent equation since Hamiltonian operator involves a time derivative, and also potential energy functions may be time dependent. However, for time independent potentials we can reduce the equation into a simpler form called **Time Independent Schrödinger Equation**. This notebook demonstrates how to approximate solutions to the time-independent Schrödinger equation for a quantum particle in a one-dimensional harmonic oscillator potential using neural networks.

## The Schrödinger Equation

The time-independent Schrödinger equation is given by:

$$
-\frac{\hbar^2}{2m} \frac{d^2\psi(x)}{dx^2} + V(x)\psi(x) = E\psi(x).
$$

where:
For simplicity, we set units such that $\hbar = 1$ and $m = 1$, reducing the equation to:

$$
-\frac{1}{2} \frac{d^2\psi(x)}{dx^2} + V(x)\psi(x) = E\psi(x).
$$
## The Harmonic Oscillator

We focus on the harmonic oscillator potential:

$$
V(x) = \frac{1}{2}x^2
$$

where we assumed unit angular frequency, i.e. $w=1$.This potential is fundamental in quantum mechanics. In fact, it is fundamental for almost all physical processes since it describes systems near stable equilibrium points.

## Neural Network Approach

### Wavefunction Representation

We represent the wavefunction $\psi(x)$ using a neural network. The network takes position $x$ as input and outputs $\psi(x)$. The wavefunction roughly can be interpreted as probability density function for the position of the particle. For example, a particle cannot be located in $x$ values where $\psi(x)=0$.

### Loss Function

The goal is to minimize the energy of the system, which is expectation value of the Hamiltonian:

$$
\text{Loss} = \frac{\langle \psi | H | \psi \rangle}{\langle \psi | \psi \rangle}
$$

### Orthogonality Constraints

To find excited states, we enforce orthogonality to all previously found wavefunctions:

$$
\int_{-\infty}^{\infty} \psi_n(x) \psi_m(x) \, dx = \delta_{nm}
$$

### Training Process

1. **Ground State:** Train the neural network to find the ground state by minimizing the energy.

2. **Excited States:** Train additional networks for excited states, adding penalties for overlaps with lower states to enforce orthogonality. In general, the next lowest energy state which is orthogonal to ground state must be first excited state in quantum systems. We can extend this property to find nth eigenstate by minimizing energy while enforcing orthogonality to all previous n-1 eigenstates.