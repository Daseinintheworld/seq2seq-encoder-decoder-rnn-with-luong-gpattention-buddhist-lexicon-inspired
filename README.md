SEQ2SEQ Reconstruction of Sanskrit Phonology via Tang-Era Siddhaṃ–Hanzi Transliteration (SRSP-TH)
Overview
This repository hosts the code and resources for the research paper, "SEQ2SEQ Reconstruction of Sanskrit Phonology via Tang-Era Siddhaṃ–Hanzi Transliteration: A Buddhist-Lexicon-Inspired Encoder–Decoder Model with Luong Attention".

The project employs a Sequence-to-Sequence (Seq2Seq) encoder–decoder model with Luong General-Product Attention to computationally reconstruct the phonetic mapping patterns used by Buddhist translators during the 7th–10th century Tang era. The model learns the complex, non-linear relationship where a single Siddhaṃ grapheme often corresponded to multiple Hanzi phonetic variants.

The core objective is to reanimate Sanskrit sounds as a learnable linguistic distribution P(y∣x) , capturing the historical balance between phonetic fidelity and metrical symmetry central to ancient transliteration practices.

Key Features & Model Architecture

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

