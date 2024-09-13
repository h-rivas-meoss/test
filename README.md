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

#### Commands

##### - get_ids : 

Retrieves a list of parcel IDs to be selected or deleted based on the presence of valid data in two tables (T060000 and T170000).

Example:

`python 001_preprocessing.py get_ids -table_a /path/to/T060000 -table_b /path/to/T170000 -id_ ID_OSS -file_type shp`
