# 📊 Data Descriptor: Layer-specific distributions of segmented cells in different cytoarchitectonic regions of BigBrain iso cortex

## Description

This dataset contains high-resolution histological image patches from the BigBrain project. Each patch represents a section of human cortex stained with the Merker method and manually annotated for cortical laminae. Cells were segmented automatically using a contour-based deep learning model.

Planned to follow BIDS (Brain Imaging Data Structure) standard with the Microscopy extension (BEP031).

---

## Folder Structure

```
my_dataset/
├── README.md
├── dataset_description.json
├── participants.tsv
├── participants.json
├── samples.tsv
├── samples.json
└── sub-01/
    └── micr/
        ├── sub-01_sample-s3467_chunk-001_BRIGHTFIELD.tif
        ├── sub-01_sample-s3467_chunk-001_BRIGHTFIELD.json
        └── (other files and chunks)
├── derivatives/
    ├── CellSegmentation/
    │   ├── dataset_description.json
    │   └── sub-01/
    │       └── micr/
    │           ├── sub-01_sample-s3467_chunk-001_desc-cellstats.tsv
    │           ├── sub-01_sample-s3467_chunk-001_desc-cellstats.json
    │           ├── sub-01_sample-s3467_chunk-001_desc-cells.tsv
    │           └── sub-01_sample-s3467_chunk-001_desc-cells.json
    │           └── (other files and chunks)
    └── Thickness/
        ├── dataset_description.json
        └── sub-01/
            └── micr/
                ├── sub-01_sample-s3467_chunk-001_desc-lamina_mask.png
                ├── sub-01_sample-s3467_chunk-001_desc-lamina_mask.json
                └── (other files and chunks)
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

---

# 📘 Dataset Description — `dataset_description.json`

```json
{
  "Name": "Layer-specific distributions of segmented cells in different cytoarchitectonic regions of BigBrain iso cortex",
  "BIDSVersion": "1.9.0",
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

| Column         | Description                             |
|----------------|-----------------------------------------|
| participant_id | BIDS participant label                  |
| species        | Species name                            |
| sex            | Biological sex                          |
| age            | Age in years (if known)                 |

Example:
```
participant_id	species	    sex	  age
sub-01	        Homo sapiens	male	65
```

### `participants.json`

```json
{
  "participant_id": {
    "Description": "BIDS participant label, e.g., sub-01"
  },
  "species": {
    "Description": "Species of the organism, here Homo sapiens"
  },
  "sex": {
    "Description": "Biological sex of the participant"
  },
  "age": {
    "Description": "Age in years (if known)"
  }
}
```

---

## 🧪 Samples

### `samples.tsv`

| Column         | Description                                    |
|----------------|------------------------------------------------|
| sample_id      | Unique ID for the histological section         |
| participant_id | Related participant                            |
| sample_type    | Biological material                            |

Example:
```
sample_id	participant_id	sample_type
s3467	    sub-01	        brain tissue
```

### `samples.json`

```json
{
  "sample_id": {
    "Description": "ID of the sample (matches sample-<label> in filename)"
  },
  "participant_id": {
    "Description": "ID of the participant (matches sub-<label> in filename)"
  },
  "sample_type": {
    "Description": "Type of biological material, e.g., 'brain tissue'"
  }
}
```

---

## 🧠 Image Metadata — `*_BRIGHTFIELD.json`

```json
{
  "Manufacturer": "Huron Digital Pathology",
  "ManufacturersModelName": "TissueScope LE120 Slide Scanner",
  "InstitutionName": "Forschungszentrum Jülich",
  "PixelSize": [1.0, 1.0],
  "PixelSizeUnits": "um",
  "Magnification": 10,
  "ImageAcquisitionProtocol": "https://github.com/FZJ-INM1-BDA/PatchExtractor",
  "OtherAcquisitionParameters": "NumericalAperture=0.75; BitDepth=8",
  "BodyPart": "BRAIN",
  "BodyPartDetails": "iso cortex",
  "BodyPartDetailsOntology": "https://www.ebi.ac.uk/ols/ontologies/uberon",
  "SampleEnvironment": "ex vivo",
  "SampleEmbedding": "Paraffin",
  "SampleFixation": "To be confirmed",
  "SampleStaining": ["Merker silver staining"],
  "SliceThickness": 20,
  "SampleExtractionProtocol": "To be confirmed",
  "SampleExtractionInstitution": "Forschungszentrum Jülich",
  "ChunkTransformationMatrix": [
    [1, 0, 0, 0],
    [0, 1, 0, 0],
    [0, 0, 1, 0],
    [0, 0, 0, 1]
  ],
  "ChunkTransformationMatrixAxis": ["X", "Y", "Z", "1"]
}
```

---

## Derivatives Folder and Files

### `derivatives/CellSegmentation/dataset_description.json`

```json
{
  "Name": "Cell-Segmentation-Pipeline for BigBrain Microscopy Data",
  "BIDSVersion": "1.9.0",
  "PipelineDescription": {
    "Name": "CPN CellSeg",
    "Version": "1.0",
    "CodeURL": "https://github.com/FZJ-INM1-BDA/celldetection",
    "Description": "Automatic cell segmentation using Contour Proposal Networks (CPN) and subsequent layer-specific cell statistics."
  },
  "HowToAcknowledge": "Upschulte et al., MedIA 2022 – Cell Segmentation via CPN",
  "SourceDatasets": [
    {
      "Name": "Layer-specific distributions of BigBrain iso cortex (Raw)",
      "URL": "https://bigbrainproject.org/"
    }
  ]
}
```

#### `sub-01_sample-s3467_chunk-001_desc-cellstats.tsv`

```
layer	cell_count	cell_size_mean_um2	cell_size_std_um2
I	    38	        89.4	            12.1
II	    54	        75.2	            10.5
III	    82	        66.7	            9.8
IV	    41	        73.5	            11.2
V	    59	        80.3	            10.7
VI	    47	        95.1	            12.5
```

#### `sub-01_sample-s3467_chunk-001_desc-cellstats.json`

```json
{
  "Description": "Layer-wise cell statistics (count and area metrics) for this patch, generated from CPN segmentation.",
  "TableColumns": {
    "layer": {
      "Description": "Cortical layer (I through VI)",
      "Levels": ["I", "II", "III", "IV", "V", "VI"]
    },
    "cell_count": {
      "Description": "Number of detected cells in this layer",
      "Units": "count",
      "DataType": "integer"
    },
    "cell_size_mean_um2": {
      "Description": "Mean cell area in square micrometers",
      "Units": "um2",
      "DataType": "float"
    },
    "cell_size_std_um2": {
      "Description": "Standard deviation of cell area in square micrometers",
      "Units": "um2",
      "DataType": "float"
    }
  },
  "GeneratedBy": {
    "Name": "CPN CellSeg v1.0",
    "CodeURL": "https://github.com/FZJ-INM1-BDA/celldetection",
    "Version": "1.0"
  }
}
```

#### `sub-01_sample-s3467_chunk-001_desc-cells.tsv`

```
cell_id	x_um	y_um	area_um2	layer
1	    12.1	34.5	87.3	I
2	    15.8	36.2	92.1	I
3	    22.4	40.8	78.5	II
...
```

#### `sub-01_sample-s3467_chunk-001_desc-cells.json`

```json
{
  "Description": "Single-cell information (position, area, layer membership) for all detected cells in this patch.",
  "TableColumns": {
    "cell_id": {
      "Description": "Unique cell identifier",
      "DataType": "integer"
    },
    "x_um": {
      "Description": "X-coordinate of the cell centroid in micrometers relative to the patch",
      "Units": "um",
      "DataType": "float"
    },
    "y_um": {
      "Description": "Y-coordinate of the cell centroid in micrometers relative to the patch",
      "Units": "um",
      "DataType": "float"
    },
    "area_um2": {
      "Description": "Cell area in square micrometers",
      "Units": "um2",
      "DataType": "float"
    },
    "layer": {
      "Description": "Cortical layer in which the cell resides (I–VI)",
      "Levels": ["I", "II", "III", "IV", "V", "VI"]
    }
  },
  "GeneratedBy": {
    "Name": "CPN CellSeg v1.0",
    "CodeURL": "https://github.com/FZJ-INM1-BDA/celldetection",
    "Version": "1.0"
  }
}
```

---

### `derivatives/Thickness/dataset_description.json`

```json
{
  "Name": "Lamina Thickness Derivative for BigBrain Microscopy Data",
  "BIDSVersion": "1.9.0",
  "PipelineDescription": {
    "Name": "ManualLaminaAnnotation",
    "Version": "1.0",
    "CodeURL": "https://microdraw.pasteur.fr",
    "Description": "Manual annotation of cortical laminae and calculation of thickness statistics."
  },
  "HowToAcknowledge": "Amunts et al., BigBrain 2013",
  "SourceDatasets": [
    {
      "Name": "Layer-specific distributions of BigBrain iso cortex (Raw)",
      "URL": "https://bigbrainproject.org/"
    }
  ]
}
```

#### `sub-01_sample-s3467_chunk-001_desc-lamina_mask.png`

*(PNG mask of the manual lamina annotation)*

#### `sub-01_sample-s3467_chunk-001_desc-lamina_mask.json`

```json
{
  "Description": "Manual annotation of cortical laminae for this patch, created by neuroanatomical experts.",
  "FileFormat": "PNG",
  "DataType": "uint8",
  "BitDepth": 8,
  "CoordinateSpace": "pixel",
  "LaminaLabels": {
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
    "MeanThickness_um": "um",
    "ThicknessStd_um": "um"
  },
  "AnnotationMethod": {
    "Type": "manual",
    "Annotators": "Trained neuroanatomists",
    "Validation": "4-eye principle (second independent review)",
    "Software": {
      "Name": "MicroDraw",
      "Version": "1.0",
      "URL": "https://microdraw.pasteur.fr"
    }
  }
}
```