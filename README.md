# Item-Based Collaborative Filtering with Hybrid Similarity

## Project Overview
This project focuses on developing a movie recommendation system utilizing Item-Based Collaborative Filtering (Item-Based CF). The primary innovation lies in moving beyond traditional rating-only based similarity by incorporating crucial movie metadata (Genre, Release Year) and a confidence measure (Rating Count) into the similarity calculation. 

The goal is to construct a robust Hybrid Similarity Matrix that enhances recommendation accuracy, improves handling of the cold-start problem, and increases content diversity compared to standard CF approaches.

## Approach and Methodology

### Core Recommendation Algorithm: Item-Based CF 

The system predicts the rating $\hat{R}_{u, i}$ a user $u$ would give to an item $i$ based on the ratings the user has given to items $j$ that are similar to $i$.The prediction formula is:$$\hat{R}_{u, i} = \frac{\sum_{j \in N(i; u)} \text{Sim}(i, j) \cdot R_{u, j}}{\sum_{j \in N(i; u)} |\text{Sim}(i, j)|}$$

Where $N(i; u)$ is the set of the $k$ most similar items to $i$ that user $u$ has already rated, and $\text{Sim}(i, j)$ is the final computed hybrid similarity between items $i$ and $j$

### Constructing the Hybrid Similarity Matrix

The core of this project is the definition of $\text{Sim}(i, j)$ as a composite metric. It combines content-based features and a statistical reliability weight to capture a more nuanced relationship between movies.

The final similarity score $\text{Sim}(i, j)$ is determined by a weighted linear combination of three distinct components:
$$\text{Sim}(i, j) = \alpha \cdot \text{Sim}_{\text{Genre}}(i, j) + \beta \cdot \text{Sim}_{\text{Year}}(i, j) + \gamma \cdot \text{Weight}_{\text{Count}}(i, j)$$ 
(Where $\alpha + \beta + \gamma = 1$ are hyperparameter weights.)

### Genre Similarity ($\text{Sim}_{\text{Genre}}$)

This component captures the intrinsic content overlap between two movies.

Calculation: It uses the Cosine Similarity between the one-hot encoded genre vectors of movie $i$ and movie $j$.

Purpose: To group movies based on their fundamental thematic and structural characteristics.

...
