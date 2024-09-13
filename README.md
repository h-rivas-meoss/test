# Overview

This folder contains a suite of applications designed to pre-process datasets generated for the **_CATALUNYA_** project. The scripts are embedded with built-in comments to track implementations. Additionally, each script can be executed via the command line with a -h option to display available commands and arguments. 

Scripts are sequentially numbered (e.g. 001_preprocessing.py) to indicate the recommended order in which they should be run.

## Features

- **Comprehensive Preprocessing:** Tools to handle ID selection, filtering, and merging of data.
- **Descriptive Statistics:** Compute various statistical measures from datasets.
- **Graphical Outputs:** Generate bar plots and time series profiles.
- **Meteorological Data Handling:** Process and visualize meteorological data over time.

## Applications

### 1. 001_preprocessing.py

#### Usage :

`001_preprocessing.py [options] [command] [args]`

This script offers several commands to manipulate and process datasets. It supports the following tasks:

#### Commands :

- get_ids : 

Retrieves a list of parcel IDs to be selected or deleted based on the presence of valid data in two tables (T060000 and T170000).

Example :

`python 001_preprocessing.py get_ids -table_a /path/to/T060000 -table_b /path/to/T170000 -id_ ID_OSS -file_type shp`

Output: 

Two lists (to_selected.txt, `to_deleted.txt`) generated in the folder containing the input tables.

- filter_ids :

Filters tables (VV, VH, NDVI, EVI...) based on a list of IDs.

Example :

`python 001_preprocessing.py filter_ids -input_dir /path/to/tables -id_ ID_OSS -list_id /path/to/`to_deleted.txt` -file_type shp -sensor s2`

This deletes the parcels present in `to_deleted.txt` from a table. All tables in the folder are automatically filtered.

- merge_tables :

Merges tables with similar names from two directories.

Example :

`python 001_preprocessing.py merge_tables -input_dir_a /path/to/dir_a -input_dir_b /path/to/dir_b -axis_ 0 -out /path/to/output_dir -file_type shp -id_ ID_OSS -id_new ID_OSSS`

This merges tables with similar names (e.g. VH_T060000) coming from two different directories (e.g. utm30 and utm31). All tables (VV, VH, NDVI, EVI...) in both directories are automatically merged.

- get_ids_extremes :

Identifies parcels with extreme values (e.g. NDVI > 1.0).

Example :

`python 001_preprocessing.py get_ids_extremes -table_a /path/to/table_NDVI -max_value 1.0 -id_ ID_OSSS -file_type shp`

This create a list of parcel IDs (to_deleted_extremes.txt) that have at least one date with an NDVI value greater than 1.0. The IDs coming from all tables (NDVI, EVI...) are written in a common file. Evaluated tables are only those with optical data. 

- filter_ids_extremes :

Filters out parcels with extreme values from tables.

Example :

`python 001_preprocessing.py filter_ids_extremes -input_dir /path/to/tables -id_ ID_OSSS -list_id /path/to/to_deleted_extremes.txt -file_type shp -sensor s2`

This deletes the parcels present in to_deleted_extremes.txt from a table. All tables in the folder are automatically filtered.

### 2. 002_stats.py

#### Usage :

`002_stats.py [options] [args]`

This script calculates descriptive statistics for a specified variable (e.g. area) from an input table.

Example :

`python 002_stats.py -input_path /path/to/input/table -output_path /path/to/output/table -subset_list 'crop_type irr_insitu area' -group_list 'crop_type irr_insitu' -col_value 'area' -file_type shp`

This calculate statistics using the variable 'area' from a given input table (e.g. VH_T060000). Statistics are calculated for each combined group based on group_list.    

### 3. 003_barplot.py

#### Usage :

`003_barplot.py [options] [args]`

Generates bar plots from a table, grouping values by specified columns.

Example :

`python 003_barplot.py -input_dir /path/to/directory -output_path /path/to/output/file.png -variable 'area' -group1 'crop_type' -group2 'irr_insitu' -nrows_ncols '2 3'`

This creates a graph from each table in the directory. Each table corresponds to a given year. The values correspond to the variable 'area'. The figure will have 2 rows and 3 columns. Values will be regrouped based on groups 1 and 2. 

### 4. 004_profil_single_crop.py

#### Usage :

`004_profil_single_crop.py [options] [args]`

Creates a time series profile graph for a single crop.

Example :

`python 004_profil_single_crop.py -input_dir /path/to/2018 -year 2018 -output_path /path/to/output/2018 -pattern '*/*filtered_merged_wgs84_filtered_extremes.shp' -group_list 'crop_types irr_insitu' -file_type shp`

This creates a graph from each table in the folder. Each table corresponds to a given index (VV, VH, NDVI, EVI...). Values will be regrouped based on group_list.

### 5. 005_profil_all_crops.py

#### Usage :

`005_profil_all_crops.py [options] [args]`

Creates a time series profile graph for all crops combined.

Example :

`python 005_profil_all_crops.py -input_dir /path/to/2018 -year 2018 -output_path /path/to/grouped/2018 -pattern '*/*filtered_merged_wgs84_filtered_extremes.shp' -group_list 'crop_types irr_insitu' -file_type shp`

This creates a graph from each table in the folder. Each table corresponds to a given index (VV, VH, NDVI, EVI...). Values will be regrouped based on group_list.

### 6. 006_meteo.py

#### Usage :

`006_meteo.py [options] [args]`

Processes meteorological data to create visualizations (e.g. temperature, precipitation).

Example :

`python 006_meteo.py -input_dir /path/to/data_meteo -output_path /path/to/output -new_cols 'date t_mean p_cum' -station_mode 'all' -t_freq 'monthly' -curve_mode 'raw' -t_window 'summer'`

This creates a graph from temperature and precipitation variables. Records from all stations are grouped by year. Raw values are aggregated monthly from May to September. 

## Notes

- Use the -h option with any command to get additional help.
- Ensure the proper execution order based on the numbering of scripts.





