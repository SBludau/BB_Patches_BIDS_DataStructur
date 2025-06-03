
# 📊 Data Descriptor: Layer-specific distributions of segmented cells in different cytoarchitectonic regions of BigBrain iso cortex

## Description

This dataset contains high-resolution histological image patches from the BigBrain project. Each patch represents a section of human cortex stained with the Merker method and manually annotated for cortical laminae. Cells were segmented automatically using a contour-based deep learning model.

All data follows the BIDS (Brain Imaging Data Structure) standard with the Microscopy extension (BEP031).

---

## Folder Structure

```
my_dataset/
├── dataset_description.json         # Metadata and software references
├── participants.tsv                 # Information about the BigBrain donor (sub-01)
├── samples.tsv                      # List of samples (histological sections)
└── sub-01/
    └── micr/
        ├── sub-01_sample-sXXXX_chunk-YYY_BRIGHTFIELD.tif       # Raw brightfield image
        ├── sub-01_sample-sXXXX_chunk-YYY_BRIGHTFIELD.json      # Metadata for the image
        ├── sub-01_sample-sXXXX_chunk-YYY_mask-lamina.png       # Manual lamina mask
        ├── sub-01_sample-sXXXX_chunk-YYY_mask-lamina.json      # Metadata for the mask
        ├── sub-01_sample-sXXXX_chunk-YYY_cellstats.tsv         # Layer-wise cell statistics
        ├── sub-01_sample-sXXXX_chunk-YYY_cellstats.json        # Metadata for cellstats
        ├── sub-01_sample-sXXXX_chunk-YYY_cells.tsv             # Per-cell position and size
        ├── sub-01_sample-sXXXX_chunk-YYY_cells.json            # Metadata for cells.tsv
```

---

## File Naming Convention

Each file follows the format:
```
sub-<participant>_sample-<section>_chunk-<patch>_<suffix>.<ext>
```

Example:
```
sub-01_sample-s3467_chunk-001_BRIGHTFIELD.tif
```

---

## Summary

- **Participant:** `sub-01` = BigBrain individual
- **Samples:** sXXXX = histological sections
- **Chunks:** image patches within each sample
- **Total chunks:** 940





# 📘 Dataset Description — `dataset_description.json`

This file provides general metadata about the dataset, including authorship, software used, and references.

```json
{
  "Name": "Layer-specific distributions of segmented cells in different cytoarchitectonic regions of BigBrain iso cortex",
  "BIDSVersion": "1.9.0",
  "DatasetType": "raw",
  "License": "CC-BY-4.0",
  "Authors": [
    "Timo Dickscheid",
    "Sebastian Bludau",
    "Christian Schiffer",
    "Anna Steffens",
    "Eric Upschulte",
    "Katrin Amunts"
  ],
  "HowToAcknowledge": "Please cite our forthcoming publication (placeholder for own publication).",
  "GeneratedBy": [
    {
      "Name": "Timo's Software Pipeline",
      "Version": "1.x"
    },
    {
      "Name": "PatchExtractor",
      "Version": "1.2"
    },
    {
      "Name": "CellDetection (CPN)",
      "Version": "1.0",
      "Description": "Automated cell segmentation using Contour Proposal Networks (CPN)",
      "CodeURL": "https://github.com/FZJ-INM1-BDA/celldetection"
    },
    {
      "Name": "SIIBRA",
      "Version": "0.4.0",
      "Description": "Spatially Interactive Atlas Browser for the Human Brain",
      "CodeURL": "https://siibra.readthedocs.io/"
    }
  ],
  "ReferencesAndLinks": [
    "https://bigbrainproject.org/",
    "https://julich-brain-atlas.de/",
    "https://www.sciencedirect.com/science/article/pii/S136184152200024X",
    "https://github.com/FZJ-INM1-BDA/celldetection",
    "https://siibra.readthedocs.io/"
  ]
}
```

---


## 🧬 Participants

### `participants.tsv`
| Column         | Description                |
|----------------|----------------------------|
| participant_id | BIDS participant label     |
| species        | Species name               |
| sex            | Biological sex             |
| age            | Age in years (if known)    |

Example:
```
participant_id	species	    sex	  age
sub-01	        Homo sapiens	male	65
```

---

## 🧪 Samples

### `samples.tsv`
Each sample corresponds to a histological section from the BigBrain brain.

| Column         | Description                    |
|----------------|--------------------------------|
| sample_id      | Unique ID for the histological section |
| participant_id | Related participant            |
| sample_type    | Biological material            |
| sample_staining| Staining technique             |

Example:
```
sample_id	participant_id	sample_type	sample_staining
s3467	    sub-01	        brain tissue	Merker silver staining
```

---

## 🧠 Image Metadata — `*_BRIGHTFIELD.json`

This file describes the microscopy image, including spatial resolution and coordinate mapping to both BigBrain and MNI reference spaces.

```json
{
  "ImagingModality": "Brightfield",
  "FileFormat": "TIFF",
  "BitDepth": 8,
  "PixelSize": [
    1.0,
    1.0
  ],
  "PixelSizeUnits": "µm",
  "SliceThickness": 20,
  "SliceThicknessUnits": "µm",
  "ObjectiveMagnification": 20,
  "NumericalAperture": 0.8,
  "Sample": "s3467",
  "StainingMethod": "Merker silver staining",
  "BigBrainReferenceSpace": {
    "Coordinates": [
      123.4,
      67.8,
      3467.0
    ],
    "CoordinateDescription": "Patch coordinates in µm within the native 3D histological BigBrain volume. The z-coordinate corresponds to the slice index × slice thickness.",
    "Reference": "BigBrain (Amunts et al., Science 2013)"
  },
  "MNI152ReferenceSpace": {
    "Coordinates": [
      12.1,
      -48.3,
      27.9
    ],
    "CoordinateDescription": "Spatial coordinates after nonlinear registration to MNI152NLin2009cAsym template (ICBM 2009c Nonlinear Asymmetrical).",
    "Reference": "https://templateflow.s3.amazonaws.com/tpl-MNI152NLin2009cAsym",
    "AtlasAnnotation": [
      {
        "AtlasName": "Julich-Brain",
        "AtlasVersion": "3.1",
        "Label": "Area 44",
        "Probability": 0.85
      },
      {
        "AtlasName": "Julich-Brain",
        "AtlasVersion": "3.1",
        "Label": "Area 45",
        "Probability": 0.1
      }
    ]
  },
  "SoftwareUsed": [
    {
      "Name": "Timo's Software Pipeline",
      "Version": "1.x"
    },
    {
      "Name": "PatchExtractor",
      "Version": "1.2"
    }
  ]
}
```



## 🧱 Laminar Annotation Metadata — `*_mask-lamina.json`

This file describes the manual annotation of cortical laminae, including thickness statistics and annotation method.

```json
{
  "Description": "Manual annotation of cortical laminae in this patch, performed by trained neuroanatomists using MicroDraw. Each layer was delineated following a standardized protocol and reviewed independently (4-eye principle).",
  "FileFormat": "PNG",
  "DataType": "uint8",
  "BitDepth": 8,
  "CoordinateSpace": "same as image",
  "LabelMap": {
    "1": {
      "Label": "Layer I",
      "MeanThickness_um": 95.2,
      "ThicknessStd_um": 8.3
    },
    "2": {
      "Label": "Layer II",
      "MeanThickness_um": 102.7,
      "ThicknessStd_um": 7.9
    },
    "3": {
      "Label": "Layer III",
      "MeanThickness_um": 134.1,
      "ThicknessStd_um": 9.4
    },
    "4": {
      "Label": "Layer IV",
      "MeanThickness_um": 84.7,
      "ThicknessStd_um": 6.2
    },
    "5": {
      "Label": "Layer V",
      "MeanThickness_um": 128.9,
      "ThicknessStd_um": 10.1
    },
    "6": {
      "Label": "Layer VI",
      "MeanThickness_um": 145.0,
      "ThicknessStd_um": 12.3
    }
  },
  "Units": {
    "MeanThickness_um": "\u00b5m",
    "ThicknessStd_um": "\u00b5m"
  },
  "AnnotationMethod": {
    "Type": "manual",
    "Annotators": "Trained neuroanatomists",
    "Validation": "4-eye principle (independent second expert)",
    "Protocol": "Standardized protocol for laminar delineation in BigBrain histology",
    "Software": {
      "Name": "MicroDraw",
      "Version": "1.0",
      "URL": "https://microdraw.pasteur.fr"
    }
  }
}
```

---

## 📈 Layer-wise Cell Statistics — `*_cellstats.tsv`

This file provides a summary of cell counts and mean sizes per lamina within one patch.

```tsv
layer	cell_count	cell_size_mean_um2	cell_size_std_um2
I	38	89.4	12.1
II	54	75.2	10.5

```

---

## 🧮 Layer-wise Statistics Metadata — `*_cellstats.json`

Describes how the cell statistics were generated and includes reference to the automated segmentation algorithm used.

```json
{
  hier soll die datei ausgegeben werden!
}
```

---

## 🔬 Per-Cell Table (Sample) — `*_cells.tsv` (First 10 rows)

Each row corresponds to one detected cell, with centroid position, area, and layer label.

```tsv
cell_id	x_um	y_um	area_um2	layer
1	12.1	34.5	87.3	I
2	15.8	36.2	92.1	I

```

---

## 🧾 Per-Cell Metadata — `*_cells.json`

Describes the content and method of the per-cell data table.

```json
{
  hier soll die dateio ausgebeben werden
}
```

---



---

## 📚 References

- Amunts et al., Science 2013 – BigBrain
- Upschulte et al., MedIA 2022 – Cell Segmentation via CPN
- https://bigbrainproject.org/
- https://julich-brain-atlas.de/
- https://siibra.readthedocs.io/
