# 📊 TOPSIS-Based Evaluation of Pre-trained Text Generation Models (Hugging Face)

## 1. Introduction

Text generation is a core task in Natural Language Processing (NLP) and is widely used in applications such as chatbots, automated content writing, summarization, and conversational AI. With the availability of numerous pre-trained text generation models, selecting the most suitable model is not straightforward because performance depends on multiple conflicting factors such as speed, model size, and generation capability.

This project addresses the model selection problem using **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution)**, a multi-criteria decision-making (MCDM) technique. TOPSIS ranks alternatives by identifying the model that is closest to the ideal solution and farthest from the worst solution.

All models used in this study are **pre-trained models sourced from Hugging Face**, and no fine-tuning is performed to ensure a fair and reproducible comparison.

---

## 2. Objective

The objectives of this project are:
- To evaluate multiple pre-trained text generation models using measurable performance metrics
- To construct a decision matrix using real experimental data
- To apply the TOPSIS methodology for ranking models
- To identify the most suitable model for text generation based on multiple criteria

---

## 3. Selected Pre-trained Models

The following Hugging Face models were selected to ensure architectural diversity and practical relevance:

| Model | Architecture |
|------|-------------|
| gpt2 | Decoder-only (Causal Language Model) |
| distilgpt2 | Lightweight Decoder-only |
| EleutherAI/gpt-neo-125M | Decoder-only |
| t5-base | Encoder–Decoder |
| facebook/bart-large | Encoder–Decoder |

These models vary significantly in size, complexity, and generation capability, making them ideal candidates for a TOPSIS-based comparison.

---

## 4. Experimental Setup

### 4.1 Text Generation Prompts

To maintain consistency and fairness, the same set of prompts was used for all models:

- *Artificial intelligence is transforming the world because*
- *Climate change is a serious global problem since*
- *In the future, technology will*

Each model generated text using identical decoding constraints.

---

## 5. Evaluation Criteria

The decision matrix was constructed using the following quantitative criteria:

| Criterion | Description | Nature |
|---------|-------------|--------|
| Inference Time (seconds) | Time required to generate outputs | Cost |
| Model Size (MB) | Memory footprint of the model | Cost |
| Parameter Count (Millions) | Number of trainable parameters | Cost |
| Average Generated Text Length | Average number of generated words | Benefit |

Cost criteria are minimized, while benefit criteria are maximized.

---

## 6. TOPSIS Methodology

### Step 1: Construction of Decision Matrix

The raw performance values collected from model execution form the decision matrix:

**D = [xᵢⱼ]**

Each row represents a model and each column represents an evaluation criterion.

The decision matrix is saved as:
decision_matrix.csv


---

### Step 2: Normalization of Decision Matrix

To eliminate unit differences among criteria, vector normalization is applied:

**rᵢⱼ = xᵢⱼ / √(Σxᵢⱼ²)**

This ensures all criteria are comparable on a common scale.

---

### Step 3: Weighted Normalized Decision Matrix

Each normalized value is multiplied by its corresponding weight:

**vᵢⱼ = wⱼ × rᵢⱼ**

In this project, equal weights were assigned:
Weights = [0.25, 0.25, 0.25, 0.25]


This reflects equal importance of all criteria.

---

### Step 4: Ideal Best and Ideal Worst Solutions

- **Ideal Best (A⁺):**
  - Maximum value for benefit criteria
  - Minimum value for cost criteria

- **Ideal Worst (A⁻):**
  - Minimum value for benefit criteria
  - Maximum value for cost criteria

---

### Step 5: Separation Measures

The Euclidean distance of each alternative from the ideal best and ideal worst is calculated:

**Sᵢ⁺ = √(Σ(vᵢⱼ − Aⱼ⁺)²)**  
**Sᵢ⁻ = √(Σ(vᵢⱼ − Aⱼ⁻)²)**

---

### Step 6: TOPSIS Score (Closeness Coefficient)

The TOPSIS score is computed as:

**Cᵢ = Sᵢ⁻ / (Sᵢ⁺ + Sᵢ⁻)**

A higher value of **Cᵢ** indicates a better-performing model.

---

### Step 7: Ranking of Models

Models are ranked in descending order of their TOPSIS scores.

The final ranked results are saved as:
final_topsis_results.csv


---

## 7. Result Table Explanation

The result table contains the following columns:

| Column | Description |
|------|------------|
| Model | Name of the text generation model |
| Inference_Time | Total time required for generation |
| Model_Size_MB | Memory footprint of the model |
| Parameters_M | Number of trainable parameters |
| Avg_Text_Length | Average number of generated words |
| TOPSIS_Score | Closeness coefficient |
| Rank | Final ranking of the model |

The model with **Rank = 1** is considered the most suitable model according to the TOPSIS methodology.

---

## 8. Result Graph Explanation

A bar chart is used to visualize the TOPSIS scores of all models.
<img width="846" height="547" alt="image" src="https://github.com/user-attachments/assets/ccfde925-386b-4391-a0ce-898281bc7163" />


### Interpretation of the Graph
- Each bar represents a text generation model
- The height of the bar corresponds to the TOPSIS score
- Taller bars indicate better overall performance
- The highest bar corresponds to the top-ranked model

The graph provides an intuitive and visual confirmation of the numerical ranking obtained from TOPSIS.

---

## 9. Conclusion

This project demonstrates a systematic and objective approach to selecting pre-trained text generation models using the TOPSIS multi-criteria decision-making method. By simultaneously considering efficiency-related and quality-related factors, TOPSIS ensures a balanced and justifiable ranking.
