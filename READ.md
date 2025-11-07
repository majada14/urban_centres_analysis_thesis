# Introduction

The current implementation funtion as backbone for the analysis provided in the research project Mapping urban neighbourhoods: a data-driven approach to identify urban centres through unsupervised machine learning.

The notebooks here implemented should then be run following the structure here described.

## Datasets
The folder datasets contains the original files that refer to the data required to be extracted, namely [Bologna Open Data requests](datasets/opendata_requests.yaml) and [Openstreetmap Data requests](datasets/osmdata_requests.yaml). 
[Urban polygons](datasets/bologna_polygons.geojson) refers to the original polygons used in the analysis and extracted separately using software QGIS.

As the analysis proceed, additional datasets and subfolders are integrated as intermediate results stored for comparison assessments.

## Data extraction and preparation

As initial step, run [Data Extraction Notebook](notebooks/data_extraction/data_extraction.ipynb) to extract data points from the original sources an apply the first cleaning processes. Raw data are then stored in the dataset folder, as they are additionally used in the following analysis.

Second, run [Matrix construction Notebook](notebooks/data_extraction/distance_matrix_computation.ipynb) as it applies data preparation steps and allow to obtain the intermediate results used in the following computation. Through separate processes, the street newtork graphs are momentarily extracted and used to construct the corresponding street distance matrix for each polygon of the analysis. These newly datasets are then stored at the specific direcory `datasets/matrix_computation` as they are directly used for the following analysis.

## Data analysis: performance assessment
The algorithms are applied separately to the distance matrix and corresponding data, and the best results are assessed considering the Pareto analysis on the validation metrics computed.
Each algorithm involved respectively provide the best results for each polygon and stores them following this structure:

- [DBSCAN Notebook](notebooks/analysis_performance/explorative_dbscan.ipynb) applies DBSCAN algorithm and stores results at the [corresponding dataset](datasets/pareto_dbscan.csv).
- [DBSCAN Notebook euclidean](notebooks/analysis_performance/explorative_dbscan_euclidean.ipynb) applies DBSCAN algorithm (with euclidean distances) and stores results at the [corresponding dataset](datasets/pareto_dbscaneu.csv).
- [Louvain Notebook](notebooks/analysis_performance/explorative_louvain.ipynb) applies Louvain algorithm and stores results at the [corresponding dataset](datasets/pareto_louvain.csv).
- [Hierarchical Agglomerative Notebook](notebooks/analysis_performance/explorative_hac.ipynb) applies Hierarchical Agglomerative algorithm and stores results at the [corresponding dataset](datasets/pareto_hac.csv)

## Data analysis: visual assessment
Similarly to before, the algortihms are applied separately and on the subsets of results obtained through the performance evualtion and validation.
For the combinations of paramters selected, the actual results of the clusters are visualised and compared.
Each algorithm involved is separately applied and visualised following this structure:

- [DBSCAN Notebook](notebooks/analysis_visual/visual_dbscan.ipynb) applies DBSCAN algorithm on subset of DBSCAN combination fo parameters.
- [DBSCAN Notebook euclidean](notebooks/analysis_visual/visual_dbscan_euclidean.ipynb) applies DBSCAN algorithm (with euclidean distances) on subset of DBSCAN combination fo parameters.
- [Louvain Notebook](notebooks/analysis_visual/visual_louvain.ipynb) applies Louvain algorithm on subset of Louvain combination fo parameters.
- [Hierarchical Agglomerative Notebook](notebooks/analysis_visual/visual_hac.ipynb) applies Hierarchical Agglomerative algorithm on subset of HAC combination fo parameters.

## Results discussion: urban centre assessment
The information obtained from the visual assessment are manually reported in the form of dictionaries, to be used in the mapping process of urban centres.
The process follow as precise structure, where the appropriate clustering algorithm is applied to single combinations of results and the visual plots obtained are stored at the directory `images/` with the specific algorithm for external purposes. Following, the clusters obtained are transformed into different shapes and aggregated for the entire municipality, separately by algorithm, in order to have a complete clustering of the entire municipality. The visual results are separately stored in the folder `images/urban_centres/` for easier comparisons and evaluated through proper spatial validation metrics.

Two scripts apply the above process separately:
- [Urban centres Notebook](notebooks/results_uc/urban_centres_construction.ipynb) construct urban centres for DBSCAN (on street distance), Louvain and Hierarchical methodologies, separately for each algorithm.
- [Urban centres Notebook euclidean](notebooks/results_uc/urban_centres_construction_euclidean.ipynb) construct urban centres for DBSCAN (on euclidean distance).

