# CNN and RNN — Deliverable 2

Week 15 — Deliverable 2: **Functional Implementation + Intermediate Optimization**

This repository contains the implementation, experiments, intermediate optimization, results, and best model checkpoints for two neural network lines:

- **CNN:** texture image classification.
- **RNN:** imagined-speech classification using EEG signals.

The objective of this deliverable is to evaluate architectural, regularization, training, and preprocessing modifications and compare their effect on validation and test performance.

---

## Repository Structure

```text
cnn-rnn-deliverable-2/
│
├── CNN/
│   ├── notebooks/
│   ├── models/
│   ├── results/
│   └── figures/
│
├── RNN/
│   ├── notebooks/
│   ├── models/
│   ├── results/
│   └── figures/
│
├── report/
│
├── README.md
├── requirements.txt
├── experiment_log.csv
└── .gitignore
```

### CNN

The CNN line focuses on texture classification using eight classes (`S00–S07`).

The Deliverable 2 working subset contains **7,571 images**, using a stratified split with seed 42:

- Training: 6,056 images
- Validation: 757 images
- Test: 758 images

The evaluated CNN experiments include changes in:

- Maximum number of epochs
- Learning rate
- Dropout
- Data augmentation
- Learning-rate scheduling
- Early stopping

The best CNN configuration was **CNN-D04**, using an initial learning rate of `0.0005`.

### Best CNN Results

| Metric | CNN-D04 |
|---|---:|
| Best validation loss | 0.0408 |
| Test accuracy | 0.9868 |
| Test loss | 0.0565 |
| Macro F1-score | 0.9873 |

---

## RNN

The RNN line uses the **EEGIS imagined-speech EEG dataset**, containing **4,044 sequences** from nine classes:

- Rest
- Help
- Bathroom
- Pain
- Thanks
- Hunger
- No
- Thirst
- Yes

Each original EEG sequence contains:

- 128 time samples
- 14 EEG channels

The stratified split with seed 42 contains:

- Training: 3,235 sequences
- Validation: 404 sequences
- Test: 405 sequences

The evaluated RNN experiments include:

- Gradient clipping
- Bidirectional LSTM
- GRU
- Frequency-band signals
- Windowed frequency-band power features

The best RNN configuration was **RNN-D06**, which transformed the EEG signals into windowed band-power features before training the LSTM.

### Best RNN Results

| Metric | RNN-D06 |
|---|---:|
| Best validation loss | 2.1386 |
| Test accuracy | 0.1630 |
| Test loss | 2.1706 |
| Macro F1-score | 0.1567 |

The main RNN finding was that improving the **EEG feature representation** produced a larger benefit than simply increasing recurrent-network complexity.

---

## Experiments

A complete record of the CNN and RNN experiments is included in:

```text
experiment_log.csv
```

The log contains the experiment ID, seed, configuration, epochs, validation metrics, test metrics, and comments for each run.

A minimum of eight combined experiments was required. This repository contains:

- **5 CNN runs**
- **6 RNN runs**
- **11 total experiments**

---

## Training Curves and Error Analysis

The repository includes training and validation curves for the selected models, together with confusion matrices and error analysis.

CNN figures are located in:

```text
CNN/figures/
```

RNN figures are located in:

```text
RNN/figures/
```

For RNN-D06, the error analysis includes the ten highest-confidence incorrect predictions.

---

## Running the Notebooks

The experiments were developed and executed using **Google Colab**.

### CNN

Open:

```text
CNN/notebooks/CNN_Deliverable2.ipynb
```

Then:

1. Mount Google Drive.
2. Update the dataset path if necessary.
3. Install the dependencies listed in `requirements.txt`.
4. Run the notebook cells sequentially.

### RNN

Open:

```text
RNN/notebooks/EEGIS_RNN_Deliverable2.ipynb
```

Then:

1. Mount Google Drive.
2. Update the EEGIS dataset path if necessary.
3. Install the dependencies listed in `requirements.txt`.
4. Run the notebook cells sequentially.

---

## Model Checkpoints

The best model checkpoints are stored in:

```text
CNN/models/
RNN/models/
```

Main checkpoints:

```text
CNN/models/CNN_D04.keras
RNN/models/RNN_D06.keras
```

---

## Datasets

The full datasets are **not included in this repository** because of their size.

The notebooks expect the datasets to be available separately, and the corresponding dataset paths may need to be updated before execution.

---

## Report

The Deliverable 2 report is located in:

```text
report/
```

The report includes:

- Functional CNN and RNN implementations
- Experiment comparisons and ablations
- Training and validation curves
- Confusion matrices
- Error analysis
- Intermediate results and discussion
