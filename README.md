# EEG-Compatible Flanker Task using PsychoPy and LSL

A real-time EEG-compatible implementation of the Eriksen Flanker Task developed in PsychoPy Builder and synchronized using Lab Streaming Layer (LSL) for acquisition with the Unicorn Hybrid Black EEG device.

This project combines cognitive experimentation, real-time event synchronization, and EEG acquisition to create a complete pipeline for behavioral and neurophysiological experiments.

---

# Overview

The Eriksen Flanker Task is a classic cognitive control paradigm used to study selective attention and conflict monitoring.

Participants are required to identify the central target letter while ignoring surrounding distractor letters (flankers).

Two experimental conditions are included:

- **Congruent trials** → flankers match the target
- **Incongruent trials** → flankers differ from the target

Examples:

| Stimulus | Correct Response | Condition |
|---|---|---|
| HHHHH | F | Congruent |
| AAAAA | J | Congruent |
| HHAHH | J | Incongruent |
| AAHAA | F | Incongruent |

Incongruent trials are expected to produce increased cognitive interference, longer reaction times, and reduced accuracy.

The paradigm is designed to be compatible with EEG experiments and ERP analysis.

---

# Features

- PsychoPy Builder implementation
- Randomized Flanker paradigm
- Practice and experimental blocks
- Real-time LSL event markers
- Unicorn Hybrid Black EEG compatibility
- LabRecorder synchronization
- EEG + behavioral data acquisition
- ERP-ready experimental timing

---

# System Architecture 

The experiment synchronizes behavioral events and EEG acquisition using Lab Streaming Layer (LSL).

```text
PsychoPy Stimulus Presentation
        ↓
LSL Event Markers
        ↓
LabRecorder Synchronization
        ↓
EEG + Event Streams (.xdf)
        ↓
MATLAB / Python Analysis
```

---

# Experimental Structure

The experiment consists of:

## 1. Instructions Routine

Participants receive task instructions and response mappings:

- `F` → target H
- `J` → target A

---

## 2. Practice Block

Practice trials allow participants to become familiar with the task before the main experiment.

- 4 randomized trials
- Feedback included
- Behavioral responses recorded

---

## 3. Main Experimental Block

Main task used for behavioral and EEG data collection.

- 60 randomized trials
- 15 repetitions per condition
- Congruent and incongruent conditions

---

# Trial Structure

Each trial contains four sequential phases:

| Phase | Duration | Purpose |
|---|---|---|
| Fixation Cross | 700–1000 ms | Attentional preparation |
| Stimulus Display | Max 1500 ms | Response window |
| Feedback | 600 ms | Performance feedback |
| Inter-trial Interval | 500 ms | Temporal separation |

These timings follow standard ERP-compatible Flanker Task protocols.

---

# LSL Integration

Lab Streaming Layer (LSL) is used for real-time synchronization between cognitive events and EEG acquisition.

PsychoPy transmits event markers during stimulus presentation while the Unicorn Hybrid Black simultaneously streams EEG signals through its own LSL outlet.

Example LSL marker transmission:

```python
outlet.push_sample(['congruent'])
```

---

# Event Markers

| Marker | Meaning |
|---|---|
| congruent | Congruent stimulus |
| incongruent | Incongruent stimulus |
| correct | Correct response |
| incorrect | Incorrect response |

These markers enable precise temporal alignment between EEG activity and cognitive events.

---

# ERP Relevance

The Flanker paradigm is commonly used in EEG and cognitive neuroscience research because incongruent trials evoke conflict-related event-related potentials (ERPs).

Expected neural signatures include:

- Enhanced N200 during conflict monitoring
- P300 modulation associated with attentional processing

---

# Running the Experiment

## 1. Start Unicorn EEG streaming

- Open Unicorn Suite
- Open LSL Interface
- Start EEG stream

## 2. Open LabRecorder

- Select EEG stream
- Select PsychoPy marker stream
- Start recording

## 3. Run PsychoPy Experiment

Open:

```text
psychopy/Flanker_Task_with_LSL.psyexp
```

- Execute the experiment

## 4. Save synchronized .xdf recording

- LabRecorder stores synchronized EEG and marker streams for offline analysis

---

# Data Collection

The experiment records:

- Reaction time (RT)
- Accuracy
- Experimental condition
- Synchronized LSL event markers

Resulting `.xdf` files can be processed offline using MATLAB or Python.

---

# Potential Future Work

Possible future extensions include:

- Online ERP visualization
- Real-time classification
- Closed-loop neurofeedback
- Adaptive stimulus presentation
- Machine learning integration
- Real-time BCI applications

---

# References

- Eriksen, B. A., & Eriksen, C. W. (1974).  
  *Effects of noise letters upon the identification of a target letter in a nonsearch task.*

- Folstein, J. R., & Van Petten, C. (2008).  
  *Influence of cognitive control and mismatch on the N2 component of the ERP.*

- Peirce, J. W. et al. (2019).  
  *PsychoPy2: Experiments in behavior made easy.*

