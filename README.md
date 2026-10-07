# SHL Hiring Assessment 2026 – Grammar Scoring Engine

## Project Overview

This project was developed for the SHL Hiring Assessment 2026.

The objective is to build a machine learning based Grammar Scoring Engine for spoken English audio. The system predicts a grammar proficiency score from spoken English recordings.

The training dataset contains 769 labeled audio samples and the test dataset contains 216 audio samples. Each audio recording is approximately 45–60 seconds long.

## Problem Statement

The task is a regression problem where the input is spoken English audio and the output is a continuous grammar score between 0 and 5.

The evaluation focuses on:

- Root Mean Squared Error (RMSE) – lower is better
- Pearson Correlation – higher is better

## Approach

The solution combines acoustic, speech, and text-based information from the audio recordings.

### 1. Audio Preprocessing

- Converted audio to mono where required.
- Used a sampling rate of 16 kHz.
- Extracted duration and speech activity information.
- Analyzed pauses, speech ratio, RMS energy and other acoustic characteristics.

### 2. Handcrafted Audio Features

The audio pipeline extracts features such as:

- MFCC
- MFCC delta
- MFCC delta-delta
- Zero Crossing Rate
- RMS Energy
- Spectral Centroid
- Spectral Bandwidth
- Spectral Rolloff
- Chroma features
- Audio duration
- Speech ratio
- Pause statistics
- Words per second

### 3. Speech-to-Text

Whisper was used to transcribe the spoken English audio into text.

The transcripts were then used to derive linguistic and language-quality features.

### 4. Text Features

The text processing pipeline includes:

- Number of words
- Number of sentences
- Average sentence length
- Sentence length variation
- Short sentence ratio
- Type-token ratio
- Filler word ratio
- Repeated word ratio
- Long word ratio
- Subordinating conjunction usage
- Punctuation-based features
- Language-model based NLL features

### 5. Deep Audio Representation

Whisper encoder representations were extracted from the audio to capture higher-level speech information.

### 6. Text Embeddings

Sentence Transformer embeddings were generated using:

`all-mpnet-base-v2`

These embeddings provide a semantic representation of the transcribed speech.

### 7. Machine Learning Models

Multiple regression models were evaluated, including:

- Extra Trees Regressor
- Random Forest Regressor
- HistGradientBoosting Regressor
- Support Vector Regression
- Ridge Regression

Model performance was evaluated using cross-validation with RMSE and Pearson correlation.

### 8. Ensemble / Stacking

Predictions from different feature groups and models were combined to improve robustness.

The ensemble combines:

- Audio embeddings
- Text embeddings
- Handcrafted audio/text features

The final predictions are constrained to the valid score range of 0–5.

## Dataset

### Training Data

- 769 audio samples
- Audio sampling rate: 16 kHz
- Mono audio
- Grammar labels ranging from 0 to 5

### Test Data

- 216 audio samples
- Labels are not provided for the test set.

## Project Structure

```text
shl-hiring-assessment-2026/
│
├── SHL_Grammar_Scoring.ipynb
├── submission.csv
├── requirements.txt
├── .gitignore
└── README.md
