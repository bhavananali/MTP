## SeamlessM4T × FLEURS Evaluation Pipeline

## Overview
This project provides a complete evaluation pipeline for testing **Meta’s SeamlessM4T-v2 model** on the **FLEURS dataset** for multiple Indian languages.  
It performs **speech and text translation tasks**, saves intermediate results (text predictions and audio outputs), and computes **standard translation/ASR metrics**.

## Supported Languages
- **Full tasks (S2TT, T2TT, S2ST, T2ST)**: Telugu (`tel`), Urdu (`urd`)
- **Partial tasks (S2TT, T2TT only)**: Tamil (`tam`), Odia (`ory`)

## Pipeline Tasks
For each parallel sentence pair in FLEURS, the following tasks are run:
- **S2TT** (Speech-to-Text Translation): Hindi speech → Target language text  
- **T2TT** (Text-to-Text Translation): Hindi text → Target language text  
- **S2ST** (Speech-to-Speech Translation, full tasks only): Hindi speech → Target language speech (`.wav`, decoded with ASR)  
- **T2ST** (Text-to-Speech Translation, full tasks only): Hindi text → Target language speech (`.wav`, decoded with ASR)  

## Outputs
- **CSV Files** per language containing:
  - Source text (Hindi transcription)
  - Reference target text
  - Predictions from each task (S2TT, T2TT, S2ST-ASR, T2ST-ASR)
- **Audio Files** stored in:
  - `input_audios/`
  - `s2s_outputs/`
  - `t2s_outputs/`

## Metrics Computed
For each language, the following metrics are reported:
- **S2TT & T2TT (Text outputs)**:
  - SacreBLEU
  - chrF2++
  - Word Error Rate (WER)
- **S2ST & T2ST (Speech outputs via ASR)**:
  - SacreBLEU
  - WER

## Requirements
See `requirements.txt` for dependencies.

Quick install:
```bash
pip install -r requirements.txt
```

## Execution Flow
1. Load source (Hindi) and target language test sets from FLEURS.  
2. Align parallel sentences using `id`.  
3. Run SeamlessM4T inference for the required tasks.  
4. Save outputs (CSV + audio).  
5. Compute and print metrics.  

## In Short
This pipeline evaluates SeamlessM4T translations for **Hindi → {Telugu, Urdu, Tamil, Odia}**, runs 4 speech/text translation tasks, saves outputs, and computes BLEU, chrF2++, and WER metrics.
