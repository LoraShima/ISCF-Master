# Multimodal Deep Learning for Electrical Motor Fault Diagnosis

## Project Overview

Electrical motors are essential components of many industrial systems, and their reliable operation is important for preventing unexpected failures, reducing maintenance costs, and improving operational efficiency.

This project investigates the use of **deep learning for electrical motor fault diagnosis**, focusing on the analysis of **vibration and acoustic signals** under different operating conditions.

The main objective is to develop a **robust multimodal fault diagnosis system** that combines information from vibration and sound signals to accurately identify motor health conditions, including when the motor operates at speeds not encountered during training.

The project is developed as part of the **Master's program in Complex Systems Engineering (ISCF-AOS)** at the Université de Technologie de Compiègne (UTC).

## Dataset

The project uses the **HUSTmotor dataset**, which contains vibration and acoustic measurements collected from electrical motors under different health conditions and operating speeds.

For our experiments, we consider:

- **6 motor health conditions** for classification.
- **4 operating speeds:** 5 Hz, 10 Hz, 20 Hz, and 30 Hz.
- **1024-point signal windows** used as inputs to the deep learning models.
- **Vibration and acoustic modalities**, analyzed independently before multimodal integration.

The dataset is preprocessed and organized to evaluate how well models generalize to previously unseen operating conditions.

## Methodology

Our approach consists of three main stages:

### 1. Data Preprocessing

Raw vibration and acoustic signals are segmented into fixed-length windows and prepared for model training.

The experimental setup follows a **domain-generalization approach**, where models are trained on data from three operating speeds and evaluated on a fourth, unseen speed.

Four evaluation tasks are considered:

| Task | Unseen Operating Speed |
|---|---|
| Task 9 | 5 Hz |
| Task 10 | 10 Hz |
| Task 11 | 20 Hz |
| Task 12 | 30 Hz |

This setup allows us to investigate whether the models learn generalizable fault-related features rather than patterns specific to individual operating speeds.

### 2. Vibration-Based Fault Diagnosis

Three deep learning architectures have been implemented and evaluated using vibration signals.

**1-D CNN**

A conventional one-dimensional convolutional neural network containing four convolutional blocks. It progressively extracts vibration features and uses a flattened feature representation for classification.

**1-D ResNet**

A residual convolutional neural network that introduces skip connections to support deeper feature extraction and improve gradient flow. Global average pooling is used to summarize the extracted features before classification.

**MSK-1DCNN**

A multiscale convolutional neural network that uses parallel convolution kernels of sizes 3, 7, and 15. These kernels capture vibration patterns at different temporal scales, and their outputs are combined to produce a feature representation for classification.

All three models are evaluated under the same experimental protocol, using 10 independent runs per task and 50 training epochs.

### 3. Acoustic and Multimodal Fault Diagnosis

Acoustic signals provide complementary information about motor behavior and can capture fault-related patterns that may not be fully represented by vibration measurements.

The project also investigates acoustic-based classification models and aims to combine the two modalities through multimodal learning.

The multimodal stage will explore how information from vibration and acoustic signals can be integrated to improve classification accuracy and robustness across operating conditions.

## Experimental Results

The following table summarizes the mean test accuracy of the three vibration-based models, compared with the vibration-only M1 baseline reported in the HUSTmotor reference paper.

| Task | Paper M1 | CNN | ResNet | MSK-1DCNN |
|---|---:|---:|---:|---:|
| Task 9 | 63.87% | 56.85% | 54.33% | 49.92% |
| Task 10 | 73.31% | 99.28% | 82.16% | 99.49% |
| Task 11 | 79.01% | 93.92% | 81.85% | 92.95% |
| Task 12 | 56.42% | 78.32% | 82.74% | 85.46% |
| **Average** | **68.15%** | **82.09%** | **75.27%** | **81.95%** |

The main findings are:

- The **1-D CNN achieves the highest overall average accuracy (82.09%)**.
- **MSK-1DCNN achieves a comparable average accuracy (81.95%)** and performs best on Task 12.
- **ResNet achieves 75.27% overall accuracy**, with relatively consistent results across Tasks 10–12.
- Task 9, corresponding to the unseen 5 Hz operating speed, remains the most challenging task for all three architectures.

These results suggest that more complex architectures do not necessarily lead to better generalization. Model performance may depend on architectural choices, input window length, and training hyperparameters.

The comparison with the reference paper is indicative rather than an exact reproduction, as experimental configurations may differ.

## Future Work

The next stages of the project include:

- Investigating additional deep learning architectures from research papers involving similar datasets and operating conditions.
- Optimizing model configurations, including window size, learning rate, optimizer, loss function, and convolution kernel sizes.
- Improving generalization performance, particularly for the unseen 5 Hz operating speed.
- Exploring different approaches for combining vibration and acoustic features.
- Evaluating whether multimodal learning improves fault diagnosis compared with individual modalities.

## Technologies and Tools

- **Python** — Data processing and model implementation
- **PyTorch** — Deep learning model development and training
- **NumPy** — Numerical operations and signal processing
- **Scikit-learn** — Evaluation metrics and data analysis
- **Matplotlib** — Visualization of experimental results
- **Google Colab** — Model training and experimentation
- **GitHub** — Version control and project management

## Dataset Availability

The preprocessed HUSTmotor dataset is not included directly in this repository because of GitHub's file-size limitations.

The dataset should be obtained separately and placed in the appropriate local data directory before running the experiments.

Trained model checkpoints may be included in the repository for reproducibility and further experimentation.

## References

1. Zhao et al. (2025) — HUSTmotor dataset and vibration/acoustic fault diagnosis reference study.
2. Liu et al. (2023) — 1-D ResNet architecture for vibration-based fault diagnosis.
3. Cao et al. (2020) — Multiscale 1-D CNN architecture for fault diagnosis.

The ResNet and MSK-1DCNN architectures used in this project are adaptations inspired by the referenced methods, rather than exact reproductions.

---

**Project Status:** Ongoing research and development.

**Research Focus:** Deep Learning · Fault Diagnosis · Vibration Analysis · Acoustic Analysis · Domain Generalization · Multimodal Learning
