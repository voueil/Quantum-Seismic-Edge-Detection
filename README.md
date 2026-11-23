# Seismic Imaging: Sharpening Features with Quantum Edge Detection

A quantum computing project exploring how Quantum Hadamard Edge Detection (QHED) can identify edges and fault structures in seismic images.

## Overview

Seismic imaging is used to study underground structures and identify geological features such as faults. Edge detection helps highlight sudden changes in image intensity, making these structures easier to analyze.

This project implements a simplified quantum edge detection approach using the Quantum Hadamard Edge Detection (QHED) algorithm.

## Problem Statement

The objective is to detect edges and fault-like structures in a seismic image using quantum computing techniques.

The project uses a synthetic 8 × 8 image containing three intensity layers and a vertical fault that shifts the right side of the image downward by two rows.

## Methodology

### 1. Classical Edge Detection

A classical approach is implemented as a baseline.

It calculates intensity differences between neighboring pixels in both horizontal and vertical directions. A threshold of 0.1 is used to identify edge pixels.

A Sobel filter is also included for visual comparison.

### 2. Quantum Hadamard Edge Detection (QHED)

The QHED algorithm uses quantum interference to calculate differences between neighboring pixel values.

The implementation follows three main steps:

1. **Amplitude Encoding:** Pixel intensities are normalized and encoded into the amplitudes of a quantum state.
2. **Cyclic Shift:** A shift operation moves the pixel values to compare neighboring positions.
3. **Hadamard Interference:** Hadamard gates are applied to the ancilla qubit to extract differences through interference.

The implementation uses:
- 6 data qubits to represent 64 pixels.
- 1 ancilla qubit for the Hadamard operations.
- 7 qubits in total.

The resulting amplitudes encode the differences between neighboring pixel values.

## Mathematical Background

For a normalized amplitude-encoded image vector:

\[
\alpha_i = \frac{v_i}{\|v\|}
\]

The QHED circuit extracts neighboring pixel differences through the odd-indexed amplitudes of the resulting statevector.

The relationship is:

\[
v_i-v_{i+1}
=
2\|v\|\times \text{odd amplitude}
\]

The probability of measuring the ancilla qubit in state 1 is:

\[
P(1)=
\frac{\sum_i(v_i-v_{i+1})^2}
{4\|v\|^2}
\]

### Basic QHED Circuit

- Create a four-pixel input vector.
- Encode the values using three qubits.
- Apply Hadamard, shift, and Hadamard operations.
- Extract the odd-indexed statevector amplitudes.
- Compare the quantum output with a manual NumPy calculation.

### Applying QHED to an Image

- Implement a reusable `qhed(image)` function.
- Apply the algorithm to an 8 × 8 image.
- Detect horizontal and vertical edges.
- Compare the quantum results with classical pixel differences.
- Validate the circuit using the mathematical equations.

### Noise and Measurement

- Add Gaussian noise to the input image.
- Test multiple edge-detection thresholds.
- Compare classical edge detection with quantum estimates.
- Investigate how measurement shots affect the results.
- Calculate agreement between the classical and quantum edge masks.

## Simulation and Results

The main validation results include:

- Total qubits: 7
- Classical edge pixels: 19
- Probability of measuring the ancilla in state 1: approximately 0.0349
- Agreement between quantum and classical results:
  - 1,000 shots: 96.9%
  - 10,000 shots: 100%
  - 100,000 shots: 100%

## How to Run

1. Clone the repository:

   ```bash
   git clone https://github.com/voueil/Quantum-Seismic-Edge-Detection.git
