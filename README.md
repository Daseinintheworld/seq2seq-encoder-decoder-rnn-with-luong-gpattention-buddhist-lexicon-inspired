# SEQ2SEQ Reconstruction of Sanskrit Phonology via Tang-Era Siddhaṃ–Hanzi Transliteration (SRSP-TH)
## Overview
This repository hosts the code and resources for the research paper, "SEQ2SEQ Reconstruction of Sanskrit Phonology via Tang-Era Siddhaṃ–Hanzi Transliteration: A Buddhist-Lexicon-Inspired Encoder–Decoder Model with Luong Attention".

The project employs a Sequence-to-Sequence (Seq2Seq) encoder–decoder model with Luong General-Product Attention to computationally reconstruct the phonetic mapping patterns used by Buddhist translators during the 7th–10th century Tang era. The model learns the complex, non-linear relationship where a single Siddhaṃ grapheme often corresponded to multiple Hanzi phonetic variants.

The core objective is to reanimate Sanskrit sounds as a learnable linguistic distribution P(y∣x) , capturing the historical balance between phonetic fidelity and metrical symmetry central to ancient transliteration practices.

## Key Findings
* Model learned the historical translators' phonetic-first, metrical-second priority hierarchy
* Larger model (512 units) showed higher composite fidelity despite lower phonetic fidelity — suggesting learned metrical weighting
* Rhythmic score consistently outperformed composite fidelity across both models, indicating prosodic structure is more learnable than full phonological reconstruction from this corpus
* Findings consistent with documented Tang-era practice of Xuanzang and Kumārajīva


## Dataset
The dataset was obtained from 2 primary volumes (TSIK 2133-b and TSIK 2135) within the Taishō Shinshū Daizōkyō, accessed via CBETA's digitized repository.

Dataset: Ensure the source data (Siddhaṃ sequences and corresponding Hanzi transliterations) is structured as aligned pairs.

Preprocessing: The provided scripts handle tokenization, Unicode normalization (NFC), and dynamic padding, converting sequences into the 80/10/10 train/validation/test split (2,091/261/261 samples)

## Key Features & Model Architecture

1. Model Configuration

Architecture: Bidirectional Gated Recurrent Units (Bi-GRUs) within an Encoder-Decoder framework.
Attention Mechanism: Luong's general-product (dot-product variant) attention, which dynamically weights input syllabic relevance to enhance cross-script feature alignment.
Models: Two configurations were tested:
    Model 1: 256 GRU/dense units (≈8.1M parameters).
    Model 2: 512 GRU/dense units (≈14.9M parameters).

2. Dataset & Philological Foundation

Corpus: ≈2,613 Siddhaṃ–Hanzi transliteration pairs extracted from Buddhist esoteric texts (TSIK 2133-b and 2135) within the CBETA digitized repository.
Translators: The source material reflects the work of influential figures like Kumārajīva (344–413 CE) and Xuanzang (602–664 CE).

3. Custom Evaluation Metrics

To assess linguistic validity beyond simple token-to-token accuracy, two custom metrics were developed:
Phonetic Similarity (M): Quantified using the PanPhon library's Distance class on International Phonetic Alphabet (IPA) representations of the sequences. It measures articulatory distance between predicted and ground-truth sounds.
Rhythmic Score (R): An exponential similarity function, R, which penalizes deviations in syllabic length between the source	and target sequences.
Composite Fidelity (F): A logistic combination of the normalized phonetic and rhythmic scores, reflecting the historical priority of acoustic accuracy modulated by metrical balance.

## Performance Summary

The models achieved high accuracy and robust phonetic generalization across the test set.
| Metric                     | Model 1 (256 Units) | Model 2 (512 Units) | 
|----------------------------|---------------------|---------------------|
|Test Accuracy               | 57.49%              | 57.99%              |
|Mean Phonetic Similarity    | 0.641               | 0.609               |
|Mean Cmposite Fidelity Score| 0.463               | 0.488               |

Model 2, with its larger representational capacity, provided a marginal but perceptually substantial improvement in overall fidelity by better modeling complex articulatory transitions and preserving rhythmic symmetry.

## Setup and Usage

Prerequisites-
1. Python 3.x
2. TensorFlow
3. Numpy
4. Pandas
5. PanPhon for phonetic evaluation
6. Aksharamukha for IPA normalization

Installation-
1. Clone the respitory:
    ```
    git clone https://github.com/Daseinintheworld/seq2seq-encoder-decoder-rnn-with-luong-gpattention-buddhist-lexicon-inspired.git
    cd seq2seq-encoder-decoder-rnn-with-luong-gpattention-buddhist-lexicon-inspired
    ```

2. Install the required Python packages:
```pip install -r requirements.txt```



