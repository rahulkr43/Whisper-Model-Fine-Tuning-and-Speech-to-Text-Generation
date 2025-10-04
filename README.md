# Whisper Model Fine-Tuning and Speech-to-Text Generation

## Overview

This project demonstrates how to fine-tune OpenAI’s **Whisper** model for **Hindi Automatic Speech Recognition (ASR)**.  
The goal is to prepare a Hindi audio dataset, train and evaluate the model, and measure its performance using **Word Error Rate (WER)**.  
Additionally, it explores detecting **speech disfluencies** (like “uh”, “umm”, false starts, and repetitions) and creating structured datasets for analysis.

---

## Table of Contents
- [Introduction](#introduction)
- [Dataset Description](#dataset-description)
- [Data Preprocessing](#data-preprocessing)
- [Fine-Tuning the Whisper Model](#fine-tuning-the-whisper-model)
- [Speech-to-Text Generation](#speech-to-text-generation)
- [Evaluation](#evaluation)
- [Installation](#installation)
- [Conclusion](#conclusion)

---

## Introduction

The **Whisper** model is a transformer-based model for speech recognition.  
It converts spoken audio into text and supports multiple languages.  

In this project, the **Whisper-small** model was fine-tuned on a **Hindi conversational dataset (~10 hours of audio)** and evaluated on a standard Hindi benchmark dataset.

---

## Dataset Description

The dataset consists of approximately **10 hours of Hindi audio recordings** with metadata and transcriptions.  

Each entry in the dataset includes:
- `user_id` – Anonymized speaker ID  
- `recording_id` – Unique identifier for each recording  
- `language` – “hi” (Hindi)  
- `duration` – Length of the audio file (in seconds)  
- `rec_url_gcp` – Cloud link to the raw audio file  
- `transcription_url` – Link to the transcription text  
- `metadata_url` – Optional metadata such as device type, noise level, or accent  

This dataset was used for both **training** and **evaluation** stages.

---

## Data Preprocessing

Before training, the dataset was prepared using the following steps:

1. **Audio Downloading** – Collected all audio files from provided URLs.  
2. **Format Conversion** – Converted audio files to `.wav` format (16 kHz sampling rate).  
3. **Text Normalization** – Cleaned transcriptions by removing noise, handling punctuation, and normalizing Hindi-English code-switched words written in Devanagari script.  
4. **Alignment** – Mapped each audio file to its corresponding transcription.  
5. **Feature Extraction** – Computed log-mel spectrograms required for the Whisper model.

---

## Fine-Tuning the Whisper Model

### Process

1. Loaded the **Whisper-small** pretrained model from Hugging Face.  
2. Used **WhisperProcessor** to prepare inputs (features and labels).  
3. Fine-tuned the model with the following parameters:
   - Optimizer: **Adam**
   - Learning Rate: **1e-5**
   - Batch Size: **16**
   - Epochs: **5**
4. Saved the fine-tuned model for evaluation and inference.

---

## Speech-to-Text Generation

After fine-tuning, the model was used for **speech-to-text generation** on unseen Hindi audio.

### Steps
1. Load the fine-tuned Whisper model.  
2. Pass the input audio through the model pipeline.  
3. Generate transcriptions automatically.  

The predicted text outputs were compared with reference transcripts to evaluate accuracy.

---

## Evaluation

Model performance was measured using the **Word Error Rate (WER)** metric.  
WER captures the differences between predicted and reference transcriptions in terms of substitutions, insertions, and deletions.

| Model Type                 | Dataset Used | WER (%) |
|-----------------------------|---------------|----------|
| Whisper-small (pretrained)  | FLEURS Hindi  | 83   |
| Whisper-small (fine-tuned)  | FLEURS Hindi  | 100  |

*(Replace `XX.X` with your actual results.)*

---

## Installation

To set up the environment, run the following commands:

```bash
# Clone the repository

git

# Navigate into the project


# Install dependencies
pip install -r requirements.txt
