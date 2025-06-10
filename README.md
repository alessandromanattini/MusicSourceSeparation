# Music Source Separation with Deep Learning

**Authors:** Afshinrad, Magalini, Manattini, Montanari  
**Course:** Selected Topics for Music and Acoustic Engineering  
**Date:** June 2025

## Project Overview

This project implements and compares state-of-the-art music source separation techniques using both classical signal processing approaches and deep learning models. We explore various neural network architectures including U-Net, along with traditional methods to separate individual instruments (vocals, drums, bass, other) from mixed audio recordings.

## Objectives

- Implement multiple source separation architectures ranging from classical DSP to modern deep learning
- Compare performance using standard evaluation metrics (SDR, SIR, SAR)
- Evaluate on the MUSDB18HQ dataset
- Analyze the trade-offs between model complexity and separation quality
- Provide comprehensive analysis of different approaches

## Technologies Used

- **Deep Learning:** PyTorch
- **Audio Processing:** librosa, torchaudio
- **Dataset:** MUSDB18HQ
- **Evaluation:** mir_eval, custom metrics
- **Classical DSP:** scipy, scikit-learn

## Dataset

We use the MUSDB18HQ dataset, which contains high-quality stereo recordings at 44.1 kHz. The dataset includes:
- 50 test tracks
- Each track contains stems for: mixture, drums, bass, vocals, other
- 30-second segments are extracted from each track for processing

## Implemented Methods

### 1. Classical Signal Processing Approaches

#### HPSS + REPET Method
Combines Harmonic-Percussive Source Separation with REpeating Pattern Extraction Technique:
- **HPSS decomposition** for initial harmonic/percussive separation
- **Frequency-based filtering** for bass extraction (low-pass at 200 Hz)
- **REPET-SIM algorithm** for vocal isolation using pattern repetition analysis
- **Vocal cleaning** in drum extraction to reduce artifacts

#### Non-negative Matrix Factorization (NMF)
Frequency-informed NMF approach:
- **Hierarchical processing** starting with HPSS decomposition
- **Frequency-specific NMF** for each instrument type
- **Soft masking** for artifact reduction
- **Customized frequency ranges** for optimal separation

### 2. Deep Learning Approaches

#### U-Net with LSTM
Hybrid CNN-LSTM architecture for spectrogram-based separation:
- **Encoder-decoder structure** with skip connections
- **Bidirectional LSTM** for temporal modeling
- **Multiplicative masking** for source-aware filtering
- **Spectrogram domain processing** with magnitude reconstruction

## Key Features

### Dataset Processing
- Automatic trimming of silent segments
- Consistent 30-second segment extraction
- New mixture generation from individual stems
- Comprehensive data validation

### Evaluation Framework
- BSS (Blind Source Separation) evaluation metrics
- SDR (Signal-to-Distortion Ratio) measurement
- SIR (Signal-to-Interference Ratio) analysis
- SAR (Signal-to-Artifacts Ratio) assessment
- Statistical analysis with box plots and distributions

### Visualization Tools
- Spectrogram comparison between estimated and ground truth
- Audio playback capabilities for qualitative assessment
- Comprehensive metric visualization

## Results Summary

The project provides comparative analysis of different source separation approaches:

- **Classical methods** offer computational efficiency and interpretability
- **Deep learning models** achieve higher separation quality but require training
- **Frequency-informed processing** significantly improves results across all methods
- **Temporal modeling** (LSTM) enhances performance for musical sequences

## Installation and Usage

1. Install requirements:
```bash
pip install -r requirements.txt
```

2. Download MUSDB18HQ dataset from [Zenodo](https://zenodo.org/records/3338373)

3. Place dataset in `./musdb18hq/test` directory

4. Run the notebook to:
    - Process and trim the dataset
    - Execute different separation methods
    - Evaluate and compare results

## File Structure

```
MusicSourceSeparation/
├── P8_Afshinrad_Magalini_Manattini_Montanari.ipynb
├── README.md
├── requirements.txt
├── musdb18hq/
│   └── test/
└── musdb18hq_trimmed/
```

## Evaluation Metrics

The project uses standard BSS evaluation metrics:
- **SDR**: Overall separation quality
- **SIR**: Interference suppression capability  
- **SAR**: Artifact levels in separated sources
