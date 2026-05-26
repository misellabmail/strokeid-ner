# StrokeID-NER

**The stroke-specific Named Entity Recognition (NER) dataset for Indonesian patient-generated health queries.**

## Overview

StrokeID-NER is a manually annotated NER dataset comprising 1,742 patient queries collected from Alodokter.com, Indonesia's leading digital health consultation platform. The dataset contains 6,778 annotated entity spans across four clinically grounded entity types, with near-perfect inter-annotator agreement (κ = 0.857).

## Entity Types

| Entity | Description | Example |
|--------|-------------|---------|
| **SYM** | Symptom | *lemas* (weakness), *pelo* (dysarthria), *cekot-cekot* (throbbing pain) |
| **DGN** | Diagnosis | *stroke*, *pendarahan otak* (brain hemorrhage), *stroke ringan* (TIA) |
| **TMP** | Temporal | *tiba-tiba* (suddenly), *sudah 3 hari* (for 3 days), *saat hari ke 20 puasa* |
| **RF**  | Risk Factor | *hipertensi* (hypertension), *diabetes*, *kolesterol* |

## Dataset Statistics

| Split | Queries | SYM | DGN | TMP | RF | Total Spans |
|-------|---------|-----|-----|-----|----|-------------|
| Train | 1,211 | 1,816 | 1,527 | 756 | 583 | 4,682 |
| Val   | 256   | 391   | 308   | 167 | 122 | 988   |
| Test  | 275   | 435   | 354   | 168 | 134 | 1,091 |
| **Total** | **1,742** | **2,650** | **2,192** | **1,096** | **840** | **6,778** |

## Data Format

All files are in tab-separated BIO format. Each line contains one token and its label, separated by a tab. Sentences are separated by blank lines.

```
stroke	B-DGN
ringan	I-DGN
yang	O
terjadi	O
tiba-tiba	B-TMP
```

## Files

```
data/
├── train_fixed.tsv     — Training set (1,211 queries)
├── val_fixed.tsv       — Validation set (256 queries)
└── test_fixed.tsv      — Test set (275 queries)

notebooks/
├── m1_indobert_linear.ipynb    — IndoBERT-base + Linear (M1)
├── m2_indobert_crf.ipynb       — IndoBERT-base + CRF (M2)
├── m3_xlm_roberta.ipynb        — XLM-RoBERTa-large + Linear (M3)
├── m4_indobert_large.ipynb     — IndoBERT-large + Linear (M4)
├── m5_gpt_zeroshot.ipynb       — GPT-5.4 zero-shot baseline
└── span_level_error_analysis   — Span-level comparative error analysis

annotation_guideline/
└── strokeid_ner_annotation_guideline_v5.pdf
```

## Models and Results

All models were evaluated on the held-out test set using span-level seqeval macro F1.

| Model | P | R | F1 |
|-------|---|---|----|
| GPT-5.4 (zero-shot) | 0.6762 | 0.6659 | 0.6682 |
| IndoBERT-base + Linear (M1) | 0.6976 | 0.7818 | 0.7367 |
| IndoBERT-base + CRF (M2) | 0.7017 | 0.7896 | 0.7427 |
| IndoBERT-large + Linear (M4) | 0.7264 | 0.8004 | 0.7614 |
| **XLM-RoBERTa-large + Linear (M3)** | **0.7394** | **0.8125** | **0.7726** |

## Requirements

See `requirements.txt` for the full list of dependencies.

## Data Source

Queries were sourced from the publicly available
[indonesia-medical-qna](https://huggingface.co/datasets/abid/indonesia-medical-qna)
dataset on HuggingFace, collected from Alodokter.com.

```bibtex
@misc{abid_famasya_abdillah_2026,
    author    = { Abid Famasya Abdillah },
    title     = { indonesia-medical-qna (Revision c8c08cd) },
    year      = 2026,
    url       = { https://huggingface.co/datasets/abid/indonesia-medical-qna },
    doi       = { 10.57967/hf/8356 },
    publisher = { Hugging Face }
}
```

## Citation

If you use StrokeID-NER in your research, please cite:

```bibtex
@article{cordiaz2026strokeidner,
  title   = {StrokeID-NER: A Stroke Named Entity Recognition
             Dataset for Indonesian Patient-Generated Health Queries},
  author  = {Cordiaz S, Miseri and Yaseen, Muhammad and Mozumder, Md Ariful Islam and Kim, Hee-Cheol},
  journal = {Scientific Reports},
  year    = {2026},
  note    = {Under review}
}
```

## Dataset DOI

[https://doi.org/10.5281/zenodo.20305007]

## License

This dataset is released under the
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.

## Authors

- **Miseri Cordiaz S** — Inje University (Main Author, corresponding author)
- **Muhammad Yaseen** — Inje University (Second Author, PhD Student)
- **Md Ariful Islam Mozumder** — Inje University (PhD Student)
- **Hee-Cheol Kim** — Inje University (Advisor Professor)
