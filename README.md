# AI Photomosaic Generator

A high-resolution **photomosaic generator** that reconstructs a target image using a dataset of smaller tile images.  
The system uses **computer vision feature extraction**, **KD-Tree nearest neighbor search**, and **tile diversity control** to intelligently match tiles and recreate the target image.

From a distance, the mosaic resembles the original image, while zooming in reveals the individual tile images used to construct it.

---

# Example

Input:
- Target image
- Dataset of tile images

Output:
- A photomosaic composed entirely of the tile images.

---

# Project Pipeline

```
User Input
   │
   ▼
Tile Preprocessing
   │
   ▼
Feature Extraction
(LAB Color + Histogram + Texture)
   │
   ▼
KD-Tree Tile Index
   │
   ▼
Target Image Patch Analysis
   │
   ▼
Tile Matching with Diversity Penalty
   │
   ▼
Mosaic Construction
   │
   ▼
Edge-Aware Blending
   │
   ▼
High Resolution Mosaic Output
```

---

# Key Features

## Feature-Based Tile Matching

Instead of naive pixel matching, tiles are matched using:

- Mean LAB color
- Color histograms
- Texture descriptors (Local Binary Pattern)

This produces visually accurate mosaics.

---

## KD-Tree Acceleration

Tile features are indexed using a KD-Tree for fast nearest-neighbor search.

Search complexity improves from:

```
O(P × T)
```

to approximately

```
O(P log T)
```

Where:

- **P** = number of patches in the target image  
- **T** = number of tile images

---

## Tile Diversity Control

To prevent the same tile from appearing repeatedly, a penalty term is applied:

```
score = feature_distance + λ × tile_usage
```

Tiles used frequently become less likely to be selected.

---

## Aspect Ratio Preservation

The mosaic maintains the **original aspect ratio** of the target image to avoid distortion.

---

## Edge-Aware Blending

Gaussian blending smooths tile boundaries to reduce visible seams.

---

# Technologies Used

- Python
- OpenCV
- NumPy
- Pillow
- scikit-learn
- scikit-image
- tqdm

Core techniques include:

- Feature extraction
- KD-Tree nearest neighbor search
- Local Binary Pattern (LBP) texture analysis
- Gaussian blending

---

# Installation

Clone the repository:

```bash
git clone https://github.com/ayushhgupta1/AI-Photomosaic-Generator-with-Feature-Based-Tile-Matching.git
cd AI-Photomosaic-Generator-with-Feature-Based-Tile-Matching
```

Install dependencies:

```bash
pip install opencv-python pillow numpy scikit-learn tqdm scikit-image
```

Optional (for super-resolution support):

```bash
pip install realesrgan
```

---

# Usage

Set the input paths and parameters in the script or notebook.

```
target_image_path = "path/to/target_image.jpg"
tile_folder = "path/to/tile_images"

tile_size = 90
grid_size = 100
```

Run the notebook or script to generate the mosaic.

The output will be saved in the **output/** directory.

Example:

```
output/targetname_mosaic_1.jpg
```

---

# Parameters

| Parameter | Description |
|----------|-------------|
| tile_size | Size of each tile image |
| grid_size | Number of tiles vertically |
| lambda_penalty | Controls tile repetition penalty |

Example:

```
tile_size = 90
grid_size = 100
```

Final mosaic height:

```
9000 pixels
```

---

# Project Structure

```
photomosaic-generator
│
├── notebook.ipynb
├── output/
├── tile_images/
└── README.md
```

---

# Possible Improvements

Future extensions could include:

- CLIP-based semantic tile matching
- Adaptive tile sizes for high-detail regions
- GPU acceleration
- Real-ESRGAN super-resolution enhancement
- Interactive web interface with Streamlit

---

# Applications

- Artistic photomosaics
- Creative image visualizations
- Computer vision demonstrations
- Portfolio projects for AI / CV roles

---

# Author

Ayush Kumar Gupta

---

# License

MIT License
