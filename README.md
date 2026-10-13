
# Dataset: Anxiety Level Prediction from Wrist-Worn Inertial Sensors in a Free-Living Setting

This repository stores the database from the study on estimating anxiety levels from movement-derived features. The project is part of the Digital Health research group at the Midiacom Laboratory, Universidade Federal Fluminense (UFF). We provide restricted access to the dataset, which can be requested by emailing the team:

* **Taiane Coelho** - taiane@midiacom.uff.br
* **Raphael** - raphael_m@id.uff.br
* **Ana Paiva** - paivaana@id.uff.br
* **Davi Silva Galindo** - davisg@id.uff.br
* **Esther Araújo Linhares** - araujo_esther@id.uff.br
* **Bernardo Mendes Rebello** - mendes_bernardo@id.uff.br

Below you will find information about the repository structure, experimental protocol, and available data.

---

# 1. Data Collection and Sensors

Participants' data are collected in a free-living setting (uncontrolled environment) and recorded continuously for a minimum of 24 hours, encompassing the participant's habitual daily routine and sleep periods.

To capture movement-derived features associated with anxiety states, monitoring primarily relies on the following wrist-worn inertial sensors (smartwatch):

* **Accelerometer** : Primary sensing modality for data acquisition; measures the magnitude and direction of linear acceleration along the X, Y, and Z axes. Enables tracking of physical activity patterns, tremors, and overall agitation throughout the participant's day.
* **Gyroscope** : Complements the accelerometer by capturing angular velocity across three rotational axes. Enables the distinction of specific wrist postures and movements relevant to anxiety-related motion patterns.

The **sampling rate** adopted on the device for all sessions and dataset versions (legacy and current models) is  **0.1 Hz** , corresponding to  **one sample per 10 seconds** .

## Free-Living Data Collection Protocol

This study was approved by the Research Ethics Committee (CAAE: 75923323.1.0000.5243) and follows CNS Resolution No. 466/2012.

Participants were recruited through announcements on social media and flyers posted at Universidade Federal Fluminense (UFF) premises. Following prior scheduling with the responsible researcher, each participant underwent an initial intake interview to:

* Sign the Informed Consent Form (Termo de Consentimento Livre e Esclarecimento — TCLE)
* Sign the Consent and Responsibility Agreement
* Complete a health screening form
* Complete validated mental health questionnaires covering the preceding two-week period, to assess inclusion/exclusion criteria
* Be assigned a de-identified numeric code (in compliance with the Brazilian General Data Protection Law — LGPD, Law No. 13,709/2018)

During the intake interview, participants were instructed on proper smartwatch usage. The minimum data collection period was  **24 consecutive hours** , during which participants maintained their habitual daily routines (including physical activities, household tasks, and normal sleep patterns).

At the end of the collection period, participants met again with the responsible researcher to:

* Complete a feedback form
* Return the device
* Transfer data stored on the smartwatch to the Midiacom Laboratory workstation
* Integrate data into a database made available to the scientific community under restricted and controlled access

# 2. Raw Data Structure and Pre-processing

Data acquired by the inertial sensors (accelerometer and gyroscope) are stored in text files on the device and subsequently transferred in **.csv** format for analysis and distribution.

## Data Dimensions and Characteristics

Signals from the accelerometer and gyroscope are temporally aligned using timestamps, yielding **six-dimensional feature vectors** for each time instant:

* **Linear acceleration (X, Y, Z)** — Accelerometer signals representing the magnitude and direction of acceleration along three axes, in m/s²
* **Angular velocity (X, Y, Z)** — Gyroscope signals representing wrist rotation and inclination across three axes, in degrees/second

## Pre-processing

Data pre-processing was performed to structure raw signals into temporal sequences suitable for machine learning analysis and modeling:

* **Synchronization and sensor fusion** — Temporal alignment of accelerometer and gyroscope signals using timestamps
* **Normalization** — Feature scaling of raw sensor readings to a standardized range
* **Sliding-window segmentation** — Partitioning of continuous signals into fixed-length temporal windows for time-series analysis
* **Filtering** — Application of temporal filters (median filter, moving-average filter) for noise reduction

Pre-processed and synchronized data are provided in **.csv** format containing the following fields:

* **datetime** — Timestamps in standardized *datetime* format recording the exact moment of each reading
* **xacc, yacc, zacc** — Accelerometer signals along the X, Y, Z axes
* **xgyro, ygyro, zgyro** — Gyroscope signals along the X, Y, Z axes

## How to Load and Manipulate the Files

Data are organized in columns corresponding to the six inertial signals, with a *datetime* index. CSV files can be loaded using any data analysis framework (pandas, NumPy, R, MATLAB, etc.). The tabular structure allows standard operations such as filtering, aggregation, and temporal analysis as required by downstream research tasks.

# 4. Reference Model Architecture

To validate this dataset, a predictive model was developed and evaluated to estimate psychometric anxiety scores from accelerometry measurements through regression.

* **Architecture** — Long Short-Term Memory (LSTM) recurrent neural network for regression.
* **Structure** — Two stacked LSTM layers (64 and 32 units), followed by a dropout layer (rate = 0.4), batch normalization, and a final linear dense output layer. The model is optimized using mean squared error (MSE) loss and the Adam optimizer.
