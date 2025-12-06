# 🎵 Audio Decomposition with SVD

> *Hearing the Mathematics of Sound*

An interactive Jupyter notebook demonstrating **Singular Value Decomposition (SVD)** applied to real audio data. Decompose sound into its fundamental "audio atoms" and explore how much information can be discarded while preserving what we hear.

To interact with this notebook, you can use the notebook here: https://colab.research.google.com/drive/1mA7Th30YtRMqi1xqK6vc7dSshFNpb0-S?usp=sharing

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![NumPy](https://img.shields.io/badge/NumPy-2.0+-green.svg)
![Librosa](https://img.shields.io/badge/Librosa-0.11+-purple.svg)

---

## The Key Insight

A **spectrogram** is simply a matrix $M \in \mathbb{R}^{F \times T}$ where:
- **Rows** = frequency bins (what pitches are present)
- **Columns** = time frames (when things happen)  
- **Values** = magnitude (how loud each frequency is at each moment)

SVD gives us:

$$M \approx \sum_{i=1}^{k} \sigma_i \, u_i \, v_i^\top$$

Each term is a **rank-1 pattern**:
- $u_i$ = "frequency profile" (which frequencies are involved)
- $v_i$ = "time activity" (when it happens)
- $\sigma_i$ = importance weight

As we increase $k$, we literally add more "audio atoms" back into our reconstruction!

## The Math

### Short-Time Fourier Transform (STFT)
Converts the 1D audio waveform into a 2D time-frequency representation by:
1. Sliding a window across the signal
2. Computing the FFT at each position
3. Stacking the results into a matrix

### Singular Value Decomposition
For our magnitude spectrogram $M$:

$$M = U \Sigma V^\top$$

Where:
- $U \in \mathbb{R}^{F \times r}$ — Left singular vectors (frequency patterns)
- $\Sigma \in \mathbb{R}^{r \times r}$ — Diagonal matrix of singular values
- $V^\top \in \mathbb{R}^{r \times T}$ — Right singular vectors (time patterns)

### Low-Rank Approximation
By keeping only the top $k$ singular values:

$$M_k = U_k \Sigma_k V_k^\top \approx M$$

The **Eckart-Young theorem** guarantees this is the optimal rank-$k$ approximation!

---

## Results Preview

For typical music (like "Running Through Me"):

| Energy Captured | Components Needed | Compression Ratio |
|-----------------|-------------------|-------------------|
| 90%             | ~16               | ~64:1             |
| 95%             | ~28               | ~37:1             |
| 99%             | ~76               | ~13:1             |

*The human ear is remarkably tolerant of aggressive SVD compression!*
