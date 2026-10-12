# StuntingMapID: Interactive Clustering Dashboard for Indonesian Provinces

## Overview
StuntingMapID groups Indonesia's 34 provinces according to their stunting-related socioeconomic and health characteristics, then makes the results explorable through an interactive dashboard. The project applies multiple clustering methods to seven indicators tied to stunting (prevalence, poverty, maternal health, sanitation, and water and healthcare access) and validates the resulting clusters statistically before translating them into an intervention-priority framework.

## Objectives
- Group Indonesian provinces by similarity in stunting-related characteristics using cluster analysis.
- Compare Hierarchical Clustering (single, complete, average, and Ward's linkage) against K-Means to identify the most reliable grouping method.
- Build an interactive dashboard that turns clustering results into a practical tool for prioritizing stunting-reduction interventions.

## Data
- Secondary data for 2023 from Statistics Indonesia (BPS) and the Ministry of Health.
- Seven variables: stunting prevalence, population aged 15+ without a primary school diploma, percentage of poor population, prevalence of chronic energy deficiency (KEK) among pregnant women, access to proper sanitation, access to proper drinking water, and access to basic health services.
- After removing 4 provinces with missing values, 34 of 38 provinces were retained for analysis.

## Methodology
1. Data validation and reconciliation: checked for duplicate province entries, quantified missing values per variable, and removed incomplete rows to ensure a clean and consistent analysis base.
2. Standardization of all numeric variables via z-score transformation, followed by a multicollinearity check (VIF, all values below 10).
3. Euclidean distance matrix computed across all province pairs as the basis for clustering.
4. Four Hierarchical Clustering methods and K-Means were each run and compared using silhouette scores across cluster counts (k = 2 to 7), supported by dendrogram and pairplot visualizations.
5. Cluster quality evaluated using within-cluster variation (Sw), between-cluster variation (Sb), and the Sw/Sb ratio; the best method was further validated with multiscale bootstrap resampling to confirm cluster stability.
6. Provinces ranked into risk tiers and intervention priorities based on an equally weighted composite of all seven indicators.

## Key Findings
- Complete Linkage with 5 clusters produced the most statistically and practically sound grouping, combining the lowest Sw/Sb ratio (0.263) among hierarchical methods with bootstrap-confirmed stability (AU > 95% for 2 of 5 clusters, moderate stability for the rest).
- Cluster 1 (5 provinces, including Nusa Tenggara Timur and Papua-region provinces) shows the highest stunting prevalence (19.6%), highest poverty (17.6%), and lowest sanitation and basic healthcare access, making it the top intervention priority.
- Cluster 4 (11 provinces) shows the most favorable profile overall, with the lowest stunting prevalence (13%) and highest access to clean water (92%), representing the lowest intervention priority.
- K-Means clustering was also tested but showed a higher Sw/Sb ratio (2.265) than all hierarchical methods, reinforcing Complete Linkage as the preferred approach for this dataset.

## Business/Government Relevance
The five-tier priority ranking gives policymakers a data-driven basis for sequencing stunting interventions rather than applying a uniform national approach. Provinces in the highest-risk clusters can be targeted first for maternal nutrition programs, poverty alleviation, and sanitation infrastructure, while lower-risk provinces can shift toward maintenance and quality-of-service improvements. The public dashboard supports transparency by letting anyone verify which province belongs to which cluster and why.

## Tools & Libraries
Python, scikit-learn (KMeans, hierarchical clustering, silhouette score), SciPy, statsmodels (VIF), pandas, Streamlit (dashboard), Folium (interactive map).

## Live Dashboard
- Live dashboard: https://stuntingmap.streamlit.app/

## Repository Contents
- `stunting_dataset_2023.csv` — cleaned dataset (34 provinces, 7 indicators).
- `StuntingMapID_Dashboard.py` / notebook — full analysis and Streamlit dashboard code (preprocessing, clustering, validation, visualization).
- `README.md` — project documentation in English and Indonesian.

## Limitations
Four provinces were excluded due to missing values, which slightly reduces national coverage. Cluster boundaries, while statistically validated, still reflect a chosen weighting scheme (equal weights across seven indicators) that may not capture every policy consideration relevant to a specific province.
