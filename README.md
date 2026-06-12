# Recommendation Systems for Personalized Content Discovery

## Project Overview

This project develops a personalized movie recommendation system using the Netflix Prize Dataset.

The objective is to learn user preferences from historical movie ratings and generate relevant personalized recommendations. The project compares traditional collaborative filtering techniques with latent factor models and evaluates them using both rating prediction and recommendation ranking metrics.

---

## Dataset

Netflix Prize Dataset

Dataset Characteristics:

- 100,480,507 ratings
- 480,189 users
- 17,770 movies
- Ratings on a 1–5 scale
- Rating timestamps
- Movie metadata (title and release year)

Due to computational limitations, a subset of 50,000 randomly sampled users from `combined_data_1.txt` was used.

After preprocessing and filtering:

- Ratings: 2,495,107
- Users: 36,027
- Movies: 4,322
- Sparsity: ~98.4%

---

## Problem Statement

Build a recommendation system capable of:

- Learning user preferences
- Predicting unseen ratings
- Generating personalized recommendations
- Identifying item similarities
- Improving content discovery

---

## Exploratory Data Analysis

The following analyses were performed:

- Rating distribution analysis
- User activity analysis
- Movie popularity analysis
- Data sparsity analysis
- Rating bias analysis
- Time trend analysis

Key findings:

- More than 60% of ratings are 4 or 5 stars.
- User activity follows a power-law distribution.
- Movie popularity follows a long-tail distribution.
- The dataset is extremely sparse (~98.4%).
- Significant user rating bias exists.

---

## Data Processing Pipeline

1. Parse Netflix rating data.
2. Randomly sample 50,000 users.
3. Merge movie metadata.
4. Clean and validate ratings and dates.
5. Filter sparse users and movies.
6. Create user-wise train-test split (80/20).

---

## Train-Test Split Strategy

User-wise random 80/20 split (seed = 42)

Advantages:

- Every user appears in both train and test sets.
- No data leakage.
- Enables per-user recommendation evaluation.

Relevance Definition:

A movie is considered relevant if:

Rating ≥ 3.5

(as specified in the problem statement)

---

## Models Implemented

### 1. Global Mean Baseline

Predicts the global average rating for all user-movie pairs.

Used as a benchmark.

---

### 2. Item-Based Collaborative Filtering (IBCF)

Methodology:

- Item-item cosine similarity
- Similar movies identified from user interactions
- Ratings predicted using weighted similarities
- Top-K recommendations generated

Advantages:

- Interpretable
- Simple
- Efficient for movie recommendation tasks

---

### 3. Singular Value Decomposition (SVD)

Matrix factorization model using Scikit-Surprise.

Features:

- Learns latent user preferences
- Learns latent movie characteristics
- Models user and item biases
- Handles sparse data effectively

Best Parameters:

- n_factors = 125
- n_epochs = 20
- lr_all = 0.005
- reg_all = 0.05

---

## Evaluation Metrics

Mandatory Metrics:

- RMSE (Root Mean Squared Error)
- MAP@10 (Mean Average Precision @ 10)

Additional Metrics:

- MAE
- Within ±0.5 rating accuracy
- Within ±1.0 rating accuracy

---

## Experimental Results

| Model | RMSE | MAP@10 |
|---------|---------|---------|
| Global Mean Baseline | 1.0844 | N/A |
| Item-Based CF | 0.9561 | 0.7187 |
| SVD | 0.8938 | 0.7627 |

Additional Comparison:

| Metric | IBCF | SVD |
|----------|----------|----------|
| Within ±0.5 | 41.8% | 43.9% |
| Within ±1.0 | 72.8% | 75.3% |

SVD achieved the best performance on both rating prediction accuracy and recommendation ranking quality.

---

## Recommendation Generation

Top-K recommendations are generated for users using:

- Item-Based Collaborative Filtering
- SVD Matrix Factorization

Recommendation quality is analyzed through:

- Sample recommendations
- Success cases
- Failure cases
- Model comparison

---

## Key Insights

- Strong positivity bias exists in ratings.
- User and movie interactions follow power-law distributions.
- Extreme sparsity is the primary challenge.
- SVD handles user bias better than IBCF.
- Hybrid recommenders could further improve performance.
- Cold-start remains an open challenge.

---

## Future Improvements

- Hybrid Recommendation Systems
- Content-Based Filtering
- Neural Collaborative Filtering
- Explainable Recommendations
- Real-Time Recommendation Updates

---

## Repository Structure

```

Recommendation-Systems-for-Personalized-Content-Discovery/

├── recommendation_systems_final_code.ipynb
├── report.pdf
├── presentation_deck.pptx
├── requirements.txt
└── README.md

```

---

## Installation

Install required libraries:

```bash
pip install -r requirements.txt
```

## Reproducing Results

### Google Colab (Recommended)

1. Download or clone this repository.
2. Upload `recommendation_systems_final_code.ipynb` to Google Colab.
3. Install the required dependencies:

```bash
pip install -r requirements.txt
```

4. Download the Netflix Prize Dataset from Kaggle.
5. Create the following folder in Google Drive:

```text
MyDrive/netflix_dataset/
```

6. Place the following dataset files inside the folder:

```text
combined_data_1.txt
combined_data_2.txt
combined_data_3.txt
combined_data_4.txt
movie_titles.csv
probe.txt
qualifying.txt
```

7. Mount Google Drive in Google Colab.
8. Ensure the dataset directory path is:

```python
DATA_DIR = '/content/drive/MyDrive/netflix_dataset/'
```

9. Run all notebook cells sequentially.

The notebook will perform data preprocessing, exploratory data analysis, model training, evaluation, and recommendation generation.

## Author

Harshita Gupta

Enrollment No: 23113065

B.Tech Civil Engineering
