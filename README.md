# GeoAI Agriculture Analytics & Hotspot Detection

This project focuses on mapping agricultural boundaries across Spain. Since many fields are tightly packed, we use instance segmentation rather than semantic segmentation to accurately distinguish between adjacent plots. 

<img width="900" height="588" alt="Captura de ecrã 2026-04-07 103659" src="https://github.com/user-attachments/assets/1da517f1-73c8-490e-886b-35a209202b0b" />
<img width="917" height="582" alt="Captura de ecrã 2026-04-07 103910" src="https://github.com/user-attachments/assets/3afd8af7-c870-4c80-bfd7-7ddc133c2be8" />

Building upon that foundation, this repository contains a Python-based GeoAI pipeline designed to analyze multispectral satellite imagery (4-channel TIFFs) for precision agriculture. It calculates key agronomic indices and features an automated hotspot detection system that highlights critical field zones.

## Key Features

Unlike standard instance segmentation models that map general field boundaries, this script dynamically isolates the top 5% highest values for each index and groups neighboring pixels into clusters. It automatically draws red bounding boxes around these specific "hotspots," allowing users to instantly pinpoint areas with the highest vegetative vigor, moisture levels, and chlorophyll concentration without needing to run a heavy neural network.

### 1. Vegetation Health (NDVI)
The following block calculates the **NDVI (Normalized Difference Vegetation Index)** for our test parcel. This index uses the Near-Infrared (NIR) and Red bands to assess biomass vigor and density. The results generate a heatmap where higher values indicate healthy vegetation.

### 2. Moisture & Water Detection (NDWI)
Next, we extract the **NDWI (Normalized Difference Water Index)** by cross-referencing the <img width="923" height="598" alt="Captura de ecrã 2026-04-07 103953" src="https://github.com/user-attachments/assets/9c0132fc-8f5c-42f4-a174-ee7dbfb7fbc1" />
Green band with the NIR band. The goal of this step is to evaluate water stress and map the presence of surface water on the parcel. The areas highlighted in blue represent locations with the highest moisture index.

### 3. Chlorophyll & Nutrition (GCI)
In this step, we focus on crop nutrition through the **GCI (Green Chlorophyll Index)**. This index is directly correlated with the amount of chlorophyll in the leaves, allowing us to estimate nitrogen levels. Areas with higher values reflect plants in a strong vegetative growth phase.

### 4. Integrated Dashboard
To facilitate decision-making, the code compiles the results into an **integrated visual dashboard**. A true-color representation of the parcel (normalized RGB) is generated and placed in perspective alongside the maps of the three previously calculated agronomic indices.

### 5. Automated Hotspot Bounding Boxes
Finally, we introduce a layer of spatial automation. The algorithm analyzes each generated map, isolates the **top 5% of highest values** (greatest vigor, most water, and most chlorophyll), and automatically draws **red bounding boxes** around these critical zones to alert the end user.

<img width="923" height="598" alt="Captura de ecrã 2026-04-07 103953" src="https://github.com/user-attachments/assets/87b06b90-e36d-4009-8be2-9ba8b20a907a" />

<img width="922" height="271" alt="Captura de ecrã 2026-04-07 104000" src="https://github.com/user-attachments/assets/7d198a11-2663-44e4-a3e8-0b1003a38da4" />
---

## Installation & Setup

### Prerequisites
You will need Python installed along with the following geospatial and scientific libraries

### Data Requirements
**⚠️ Note on Dataset:** Due to GitHub's file size limits, the raw `.tif` satellite images are NOT included in this repository. 

To run this code locally:
1. Create a folder named `data/test_dir/` in the root directory.
2. Place your 4-channel (Red, Green, Blue, NIR) `.tif` satellite or drone imagery inside this folder.
3. The script will automatically fetch the first image in the directory and process it.

## Usage
Simply open the Jupyter Notebook (`.ipynb`) or run the Python script (`.py`). The script will read the raw satellite data, perform the matrix calculations, and output a matplotlib dashboard with the RGB true-color image and the three index maps highlighting the highest value zones.

---

## Acknowledgments
This work was inspired by the work of Professor Qiusheng Wu, available on his GitHub page: [https://github.com/giswqs](https://github.com/giswqs)
