# StuntingMapID: Dashboard Clustering Interaktif untuk Provinsi di Indonesia

## Ringkasan
StuntingMapID mengelompokkan 34 provinsi di Indonesia berdasarkan karakteristik sosio-ekonomi dan kesehatan yang berkaitan dengan stunting, kemudian menyajikan hasilnya melalui dashboard interaktif yang dapat dieksplorasi. Proyek ini menerapkan beberapa metode clustering pada tujuh indikator terkait stunting (prevalensi, kemiskinan, kesehatan ibu, sanitasi, serta akses air dan layanan kesehatan), memvalidasi hasil cluster secara statistik, kemudian menerjemahkannya menjadi kerangka prioritas intervensi.

## Tujuan
- Mengelompokkan provinsi di Indonesia berdasarkan kemiripan karakteristik penyebab stunting menggunakan analisis cluster.
- Membandingkan Hierarchical Clustering (single, complete, average, dan ward's linkage) dengan K-Means untuk menemukan metode pengelompokan yang paling andal.
- Membangun dashboard interaktif yang mengubah hasil clustering menjadi alat praktis untuk memprioritaskan intervensi penurunan stunting.

## Data
- Data sekunder tahun 2023 dari Badan Pusat Statistik (BPS) dan Kementerian Kesehatan.
- Tujuh variabel: prevalensi stunting, penduduk usia 15+ tidak tamat SD, persentase penduduk miskin, prevalensi ibu hamil Kekurangan Energi Kronis (KEK), akses sanitasi layak, akses air minum layak, dan akses layanan kesehatan dasar.
- Setelah menghapus 4 provinsi dengan data hilang, 34 dari 38 provinsi dipertahankan untuk analisis.

## Metodologi
1. Validasi dan reconciliation data: memeriksa duplikasi entri provinsi, menghitung jumlah missing value per variabel, dan menghapus baris yang tidak lengkap untuk memastikan dasar analisis yang bersih dan konsisten.
2. Standarisasi seluruh variabel numerik menggunakan transformasi z-score, dilanjutkan dengan pengecekan multikolinearitas (VIF, seluruh nilai di bawah 10).
3. Perhitungan matriks jarak Euclidean antar seluruh pasangan provinsi sebagai dasar clustering.
4. Empat metode Hierarchical Clustering dan K-Means masing-masing dijalankan dan dibandingkan menggunakan silhouette score pada berbagai jumlah cluster (k = 2 hingga 7), didukung visualisasi dendrogram dan pairplot.
5. Kualitas cluster dievaluasi menggunakan within-cluster variation (Sw), between-cluster variation (Sb), dan rasio Sw/Sb; metode terbaik lebih lanjut divalidasi dengan multiscale bootstrap resampling untuk memastikan stabilitas cluster.
6. Provinsi diberi peringkat risiko dan prioritas intervensi berdasarkan skor komposit dengan bobot yang sama untuk ketujuh indikator.

## Temuan Utama
- Complete Linkage dengan 5 cluster menghasilkan pengelompokan yang paling solid secara statistik maupun praktis, menggabungkan rasio Sw/Sb terendah (0,263) di antara metode hierarchical dengan stabilitas yang dikonfirmasi bootstrap (AU > 95% untuk 2 dari 5 cluster, stabilitas sedang untuk sisanya).
- Cluster 1 (5 provinsi, termasuk Nusa Tenggara Timur dan provinsi-provinsi wilayah Papua) menunjukkan prevalensi stunting tertinggi (19,6%), kemiskinan tertinggi (17,6%), serta akses sanitasi dan kesehatan dasar terendah, menjadikannya prioritas intervensi utama.
- Cluster 4 (11 provinsi) menunjukkan profil paling baik secara keseluruhan, dengan prevalensi stunting terendah (13%) dan akses air bersih tertinggi (92%), menjadikannya prioritas intervensi terendah.
- Clustering K-Means juga diuji namun menunjukkan rasio Sw/Sb yang lebih tinggi (2,265) dibandingkan seluruh metode hierarchical, memperkuat Complete Linkage sebagai pendekatan yang lebih disukai untuk dataset ini.

## Relevansi Bisnis/Pemerintahan
Peringkat prioritas lima tingkat memberikan pembuat kebijakan dasar berbasis data untuk mengurutkan intervensi stunting, alih-alih menerapkan pendekatan seragam secara nasional. Provinsi pada cluster berisiko tertinggi dapat menjadi sasaran pertama untuk program gizi ibu, pengentasan kemiskinan, dan infrastruktur sanitasi, sementara provinsi berisiko rendah dapat beralih ke pemeliharaan dan peningkatan kualitas layanan. Dashboard publik mendukung transparansi dengan memungkinkan siapa pun memverifikasi provinsi mana termasuk dalam cluster mana beserta alasannya.

## Tools & Libraries
Python, scikit-learn (KMeans, hierarchical clustering, silhouette score), SciPy, statsmodels (VIF), pandas, Streamlit (dashboard), Folium (peta interaktif).

## Dashboard Live dan Repository
- Dashboard live: https://stuntingmapid.streamlit.app/

## Isi Repository
- `stunting_dataset_2023.csv` — dataset yang sudah dibersihkan (34 provinsi, 7 indikator).
- `StuntingMapID_Dashboard.py` / notebook — kode analisis lengkap dan dashboard Streamlit (preprocessing, clustering, validasi, visualisasi).
- `README.md` — dokumentasi proyek dalam bahasa Inggris dan Indonesia.

## Keterbatasan
Empat provinsi dikeluarkan karena missing value, yang sedikit mengurangi cakupan nasional. Batas cluster, meskipun tervalidasi secara statistik, tetap mencerminkan skema pembobotan yang dipilih (bobot sama untuk ketujuh indikator) yang mungkin belum mencakup seluruh pertimbangan kebijakan yang relevan untuk provinsi tertentu.

---------------------------------------------------------------------------------

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

## Live Dashboard and Repository
- Live dashboard: https://stuntingmapid.streamlit.app/

## Repository Contents
- `stunting_dataset_2023.csv` — cleaned dataset (34 provinces, 7 indicators).
- `StuntingMapID_Dashboard.py` / notebook — full analysis and Streamlit dashboard code (preprocessing, clustering, validation, visualization).
- `README.md` — project documentation in English and Indonesian.

## Limitations
Four provinces were excluded due to missing values, which slightly reduces national coverage. Cluster boundaries, while statistically validated, still reflect a chosen weighting scheme (equal weights across seven indicators) that may not capture every policy consideration relevant to a specific province.
