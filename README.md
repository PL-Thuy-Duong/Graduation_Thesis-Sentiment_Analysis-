<h1 align="center">A Knowledge Graph for Sentiment Analysis from Image Data</h1>

## Overview

This repository contains the implementation and materials for the graduation thesis:

**“A Knowledge Graph for Sentiment Analysis from Image Data”**

The project proposes a context-aware emotion recognition framework that integrates image captioning, natural language processing, and knowledge graph modeling to analyze human emotions expressed in images.

Instead of relying solely on visual features, the proposed method explicitly models semantic context and emotional commonsense knowledge, enabling more robust sentiment analysis in complex real-world images.


## Research Motivation

Human emotion perception is highly context-dependent.

The same facial expression or posture may convey different emotions depending on surrounding objects, activities, and social interactions.

This motivates the need for:

Context-based emotion understanding

Explicit semantic reasoning beyond pixel-level features

Structured representations of emotional knowledge

This work addresses these challenges by constructing a knowledge graph from image-derived textual descriptions, enriched with external emotion knowledge.


## Research Objectives

Generate semantic captions from images containing emotional contexts.

Extract sentiment-relevant entities and relations from captions.

Construct a knowledge graph representing emotions, concepts, and their relationships.

Apply graph neural networks to perform emotion recognition.

Evaluate the effectiveness of the proposed method on the EMOTIC dataset.


## Methodology

### *1. Dataset*

EMOTIC Dataset including 23,571 images

### *2. Image Caption Generation*

Images are converted into textual descriptions using the BLIP (Bootstrapping Language-Image Pre-training) model.

Captions serve as an intermediate semantic representation bridging vision and language.

### *3. Caption Preprocessing*

Generated captions are processed through:

1. Stopword removal
2. Lemmatization
3. Filtering irrelevant or non-emotional content
    
The resulting keywords represent valid semantic units for graph construction.

### *4. Knowledge Graph Construction*

- The knowledge graph consists of the following nodes:

 1. Valid words extracted from captions
 2. Add 26 emotion categories
 3. Mood tags
 4. Related words derived from SenticNet 5 and WordNet
Each valid word retrieves:
 5. Add 5 related words from SenticNet / WordNet
Each related word further retrieves additional semantic connections

- Edge Construction
1. Word–Emotion edges: weighted using co-occurrence probability
2. Word–Word edges: based on normalized co-occurrence frequency
3. Word–MoodTag edges: derived from SenticNet pleasantness values
4. Related-word connections: weighted using polarity values from SenticNet
       
This results in a context-aware emotional knowledge graph that explicitly encodes semantic and affective relationships.

### *5. Graph Representation Learning*

GloVe 200-dimensional embeddings are used to represent node features.

Knowledge graphs are organized into batches for training.

Two graph neural network architectures are evaluated:

- GIN (Graph Isomorphism Network)
- PNA (Principal Neighbourhood Aggregation)

## Experiments & Evaluation

- Training Setup: Train / Validation / Test split: 70% / 10% / 20%
- Optimizer: AdamW
- Learning rate: 0.0001
- Epochs: 20
- Batch size: 8
- Scheduler: ReduceLROnPlateau
- Evaluation Metric
- Mean Average Precision (mAP) across emotion classes

## Results

The proposed knowledge graph-based approach outperforms the EMOTIC baseline.

PNA shows stronger performance compared to GIN in modeling complex neighborhood structures.

The method demonstrates improved robustness in scenes with:

- Multiple interacting subjects
- Occlusion
- Ambiguous visual cues

## Project Structure

Graduation_Thesis-Sentiment_Analysis/

│

├── README.md

├── .gitignore

├── requirements.txt

│

├── SourceCode/

│   ├── Captioning.ipynb

│   ├── annotation1.py

│   ├── senticnet5.py

│   ├── graph_PNA_seeding_27_50.ipynb

│   ├── caption_full.csv

│   ├── captions_train.csv

│   ├── captions_val.csv

│   └── captions_test.csv

│

├── SOFT/

│   └── requirements.txt

│

└── Thesis/

    ├── 47.01.104.074_PhanLuongThuyDuong.docx
    
    ├── 47.01.104.074_PhanLuongThuyDuong.pdf
    
    └── 47.01.104.074_PhanLuongThuyDuong.pptx
    
## External Resources

### Pre-trained Word Embeddings

This project uses GloVe 6B – 200d embeddings.

>Download from: https://nlp.stanford.edu/projects/glove/


## Limitations

Complex scenes with many objects and actions may introduce ambiguity.

Knowledge graph structure can be further enriched with:

- Facial features
- Body pose information
- Graph connectivity depends on the quality of caption generation.

## Future Work

Incorporate face and body pose branches to enrich semantic representation.

Combine Large Language Models (LLMs) with Vision-Language Models.

Improve semantic alignment between visual and textual representations.

Expand emotional commonsense knowledge sources.

## Author
Phan Luong Thuy Duong

Graduation Thesis – Ho Chi Minh City University of Education

Supervisors: Nguyen Viet Hung, PhD
             Vo Le Phuc Hau, M.Sc.

## References

Key references include EMOTIC, BLIP, SenticNet, WordNet, and recent context-aware emotion recognition studies as cited in the thesis.

