# Research-Grade EEG Stress vs Relaxation Analysis Pipeline

## Overview
This repository implements a **research-grade EEG signal processing and feature extraction framework** for distinguishing **stress vs relaxation states**. The pipeline follows **standard biomedical signal processing practices** and is suitable for **MSc theses, PhD research**. All steps are modular, reproducible, and machine-learning ready.

---

## Dataset Description
- **Input format:** CSV files (e.g., `Stressed.csv`, `Relaxed.csv`)
- **Signal type:** Single-channel EEG
- **Sampling frequency:** 128 Hz
- **Samples per subject:** 3200
- **Windowing strategy:**  
  - 1-second windows (128 samples per window)  
  - 25 windows per subject  
- **Labeling:** Binary (Stress = 1, Relax = 0)

---

## Preprocessing Pipeline
1. **Reshaping:** Raw EEG signals reshaped into fixed-length temporal windows  
2. **Normalization:** Min–Max or Z-score normalization (optional)  
3. **Filtering:**  
   - Butterworth band-pass filters  
   - EEG frequency bands:
     - Delta: 0.5–4 Hz  
     - Theta: 4–8 Hz  
     - Alpha: 8–12 Hz  
     - Beta: 12–30 Hz  
     - Gamma: 30–45 Hz  
4. **Artifact-safe segmentation:** Window-level processing ensures robustness

---

## Time-Domain Feature Extraction
Extracted per window:
- Variance
- Root Mean Square (RMS)
- Peak-to-Peak Amplitude
- Signal Energy

These features quantify **amplitude variability and signal intensity**, critical for stress detection.

---

## Frequency-Domain Analysis
- **Method:** Welch’s Power Spectral Density (PSD)
- **Extracted features per EEG band:**
  - Band power
  - Maximum power
  - Dominant frequency
- **Tooling:** `scipy.signal`, `mne_features`

---

## Hjorth Parameters
For each window:
- **Activity**
- **Mobility**
- **Complexity**

These parameters compactly describe EEG spectral dynamics and waveform complexity.

---

## Entropy-Based Features
Measures of signal irregularity and information content:
- Approximate Entropy
- Sample Entropy
- Spectral Entropy
- Singular Value Decomposition (SVD) Entropy

Entropy features are widely used in **mental workload and stress-related EEG studies**.

---

## Fractal and Nonlinear Features
- Higuchi Fractal Dimension
- Katz Fractal Dimension

These features capture **nonlinear EEG dynamics**, improving stress classification performance.

---

## Hilbert Transform Analysis
- Analytic signal generation using Hilbert Transform
- Envelope extraction for each EEG band
- Features:
  - Maximum envelope power
  - Frequency at maximum envelope response

---

## Sliding Window Spectral Analysis
- Window size: 2 seconds
- Overlap: 50%
- Purpose: Capture temporal evolution of stress patterns

---

## Dimensionality Reduction and Clustering
- **PCA:** Variance analysis and feature compression
- **KMeans Clustering:** Behavioral grouping
- **Hierarchical Clustering:** Ward linkage dendrogram
- **Validation:** Silhouette score and elbow method

---

## Output Artifacts
Generated CSV files:
- `time_domain_features.csv`
- `frequency_domain_features.csv`
- `hjorth_features.csv`
- `entropy_features.csv`
- `fractal_features.csv`
- `eeg_features.csv` (final merged dataset)

All outputs are **ML-ready** and compatible with scikit-learn, TensorFlow, and PyTorch.

---

## Technologies Used
- Python 3.x
- NumPy, Pandas
- SciPy
- MNE-Features
- scikit-learn
- Matplotlib, Seaborn

---

## Scientific Validity
This pipeline aligns with methodologies used in:
- IEEE Transactions on Biomedical Engineering
- Elsevier Neurocomputing
- Springer Brain–Computer Interfaces

Features are interpretable, reproducible, and suitable for **stress detection, affective computing, and BCI systems**.

---

## Intended Applications
- EEG-based stress classification
- Brain–Computer Interface (BCI) research
- Mental health analytics
- Cognitive workload assessment
- Biomedical signal processing research
