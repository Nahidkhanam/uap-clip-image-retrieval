
# Universal Adversarial Perturbation (UAP) for CLIP-based Image Retrieval

## Project Overview

This project presents a simplified implementation of **Universal Adversarial Perturbation (UAP)** against the **CLIP (Contrastive Language–Image Pretraining)** model for the **Image-to-Text Retrieval** task.

The objective is to generate a **single universal perturbation** that, when added to every input image, degrades the retrieval performance of CLIP while remaining visually imperceptible.

> **Note:** This is a simplified educational implementation inspired by the UAP-VLP research paper. It is **not** an exact reproduction of the official UAP-VLP repository.

---

## Features

- CLIP-based Image-to-Text Retrieval
- Flickr30K Dataset (200-image subset)
- Universal Adversarial Perturbation (UAP)
- Baseline Retrieval Evaluation
- Adversarial Retrieval Evaluation
- Recall@1, Recall@5, Recall@10 Metrics
- Training Loss Visualization
- Universal Perturbation Visualization
- Original vs Adversarial Image Comparison

---

# Dataset

**Dataset:** Flickr30K (Kaggle Version)

Original Dataset:

- 31,783 Images
- 158,915 Captions

Subset Used:

- **200 Images**
- **1000 Captions (5 captions per image)**

---

# Model

**Vision-Language Model**

- OpenAI CLIP
- ViT-B/32 Backbone

Task:

- Image-to-Text Retrieval

---

# Methodology

## Step 1 – Dataset Preparation

- Download Flickr30K dataset from Kaggle.
- Parse image-caption pairs from `results.csv`.
- Select the first 200 unique images.
- Keep all five captions corresponding to each image.

Final Dataset:

- 200 Images
- 1000 Captions

---

## Step 2 – Baseline Retrieval

For every image:

- Generate image embeddings using CLIP Image Encoder.

For every caption:

- Generate text embeddings using CLIP Text Encoder.

Normalize both embeddings before similarity computation.

Compute cosine similarity between every image and every caption.

---

## Step 3 – Retrieval Evaluation

Evaluate retrieval performance using:

- Recall@1
- Recall@5
- Recall@10

Each image has five corresponding ground-truth captions.

---

## Step 4 – Universal Adversarial Perturbation

A single perturbation **δ** is initialized.

For every training image:

1. Add universal perturbation
2. Generate adversarial image
3. Compute CLIP image embedding
4. Compare with corresponding text embeddings
5. Compute retrieval loss
6. Backpropagate gradients
7. Update perturbation
8. Project perturbation into the L∞ constraint

Only the perturbation is optimized while CLIP parameters remain frozen.

---

# Hyperparameters

| Parameter | Value |
|-----------|-------|
| Model | CLIP ViT-B/32 |
| Images | 200 |
| Captions | 1000 |
| Epochs | 10 |
| Optimizer | Adam |
| Learning Rate | 1/255 |
| L∞ Bound (ε) | 8/255 |

---

# Experimental Results

## Baseline Retrieval Performance

| Metric | Score |
|---------|------:|
| Recall@1 | **93.0%** |
| Recall@5 | **98.5%** |
| Recall@10 | **99.0%** |

---

## Retrieval Performance After UAP

| Metric | Score |
|---------|------:|
| Recall@1 | **83.5%** |
| Recall@5 | **94.0%** |
| Recall@10 | **96.5%** |

---

## Performance Degradation

| Metric | Drop |
|---------|------:|
| Recall@1 | **9.5%** |
| Recall@5 | **4.5%** |
| Recall@10 | **2.5%** |

The learned universal perturbation successfully reduces retrieval performance while maintaining minimal visual distortion.

---

# Workflow

```text
                Flickr30K Dataset
                        │
                        ▼
              Image Preprocessing
                        │
                        ▼
               CLIP Image Encoder
                        │
                        ▼
               Image Embeddings
                        │
                        ▼
             Image-Text Similarity
                        │
                        ▼
            Baseline Retrieval Metrics
                        │
                        ▼
     Initialize Universal Perturbation (δ)
                        │
                        ▼
          Generate Adversarial Images
                        │
                        ▼
               CLIP Image Encoder
                        │
                        ▼
          Adversarial Image Embeddings
                        │
                        ▼
         Image-Text Similarity Matrix
                        │
                        ▼
      Recall@1 / Recall@5 / Recall@10
````

---

# Project Structure

```text
.
├── dataset/
│   ├── flickr30k_images/
│   └── results.csv
│
├── notebooks/
│   └── UAP_CLIP_Retrieval.ipynb
│
├── outputs/
│   ├── loss_curve.png
│   ├── uap.png
│   ├── comparison.png
│   ├── baseline_similarity.png
│   ├── adv_similarity.png
│   └── results.csv
│
└── README.md

```
---

# Visual Outputs

The project generates the following visualizations:

* Training Loss Curve
* Learned Universal Perturbation
* Original vs Adversarial Images
* Baseline Similarity Matrix
* Adversarial Similarity Matrix
* Retrieval Comparison
* Recall@K Performance Comparison

---

# Technologies Used

* Python
* Google Colab
* PyTorch
* OpenAI CLIP
* NumPy
* Pandas
* Matplotlib
* PIL
* Kaggle API

---

# Key Contributions

* Implemented a CLIP-based image retrieval pipeline.
* Developed a simplified Universal Adversarial Perturbation framework.
* Evaluated retrieval performance before and after the attack.
* Demonstrated the vulnerability of CLIP-based retrieval systems to universal perturbations.
* Generated qualitative and quantitative visualizations for analysis.

---

# Limitations

This project is a simplified educational implementation inspired by the UAP-VLP paper.

The following simplifications were made:

* A subset of 200 images was used instead of the complete Flickr30K dataset.
* Only the CLIP ViT-B/32 model was evaluated.
* A simplified optimization objective was used instead of the complete UAP-VLP loss.
* Cross-model transferability was not evaluated.

---

# Future Work

Potential future improvements include:

* Implementing the complete UAP-VLP optimization objective.
* Evaluating on the full Flickr30K dataset.
* Testing transferability across multiple vision-language models.
* Extending the attack to image captioning and visual grounding.
* Comparing multiple universal adversarial attack methods.

---

# Acknowledgement

This project is inspired by research on **Universal Adversarial Perturbations for Vision-Language Models**. It is intended for educational and research purposes to demonstrate the impact of universal perturbations on CLIP-based image retrieval systems.

```
```
