# Lab CH22 — Unsupervised Learning: Clustering Economies

## P — Purpose
Cluster ~160 countries using World Bank development indicators to discover
natural economic groupings without using income labels. Evaluate whether
unsupervised K-Means clustering can reproduce the World Bank's own
four-tier income classification system.

## R — Role
Machine Learning student applying unsupervised learning techniques to
real-world economic data. Tools used: Python, scikit-learn, wbgapi,
matplotlib, seaborn, pandas.

## I — Instructions
This lab walks through the full unsupervised learning pipeline:
1. Fetch 10 development indicators for ~160 countries via the World Bank API
2. Standardize features using StandardScaler
3. Fit K-Means (K=4) and visualize clusters with PCA
4. Evaluate cluster quality using the Elbow Method and Silhouette Score
5. Compare discovered clusters to World Bank income group labels
6. Extension: Peer debate on K=3 vs K=5
7. Challenge: Apply clustering to California Housing dataset

## M — Methods & Concepts
| Concept | Description |
|---|---|
| K-Means | Partitions n observations into K clusters by minimizing WCSS |
| StandardScaler | Transforms features to mean=0, std=1 before clustering |
| PCA | Reduces dimensions to 2D for cluster visualization |
| Elbow Method | Plot WCSS vs K — look for the bend |
| Silhouette Score | Measures cluster cohesion vs separation. Range [-1, 1] |
| Cross-tabulation | Compares cluster labels to known income group labels |

## E — Evaluation
- **Part 3:** K-Means fitted with K=4, PCA scatter shows well-separated clusters
- **Part 4:** Elbow bends around K=3–4; silhouette score confirms K=4 is reasonable
- **Part 5:** Heatmap shows strong alignment between K-Means clusters and World Bank income tiers — demonstrating that unsupervised learning can recover economically meaningful structure
- **Challenge:** California Housing clustered into 4 groups with geographic and economic interpretation

## Dataset
- **World Development Indicators** via `wbgapi` — 10 indicators, ~160 countries
- **California Housing** via `sklearn.datasets`

## How to Run
1. Open `lab-ch22-guided.ipynb` in Google Colab or VS Code
2. Run cells top-to-bottom with Shift+Enter
3. All dependencies install automatically in Cell 1

## Files
| File | Description |
|---|---|
| `lab-ch22-guided.ipynb` | Main notebook with all solutions |
| `pca_clusters.png` | PCA scatter plot colored by cluster |
| `elbow_silhouette.png` | Elbow + silhouette plots for K=2–10 |
| `cluster_income_heatmap.png` | Heatmap of clusters vs income groups |
| `cluster_debate.png` | K=3 vs K=5 comparison |
| `housing_map.png` | California Housing geographic cluster map |
| `housing_labeled_map.png` | California Housing with economic labels |

## Author
Machine Learning — Lab Chapter 22
