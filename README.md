# iAAA-MRI-Challenge

> Unzip data file [`MRI_Labeling_normal_abnormal_SPI_p0_s0.zip`](./MRI_Labeling_normal_abnormal_SPI_p0_s0.zip), the data structure is as shown below:

```
MRI_Labeling_normal_abnormal_SPI_p0_s0
├── data
├── label
└── labels_dictionary.json
```


### Data Structure

1. `labels_dictionary.json`

> This file is a metadata for labels, it contains **label_name**, **label_type**, and **pixel_value** that exists in the mask file.


```json
{
    "normal": {
        "value": 1, 
        "type": "classification/tag"
    }, 
    "abnormal": {
        "value": 2, 
        "type": "classification/tag"
    }, 
    "corrupted": {
        "value": 3, 
        "type": "classification/tag"
    }
}
```

2. `data` directory

> This folder contains raw DICOM series. Each `XNAT_Exxxxx` directory contains a study belonging to one patient, which includes **3 series**: `[T1W_SE, T2W_TSE, T2W_FLAIR]`. Each series has [16-18] slices.

```
data
├── XNAT_E09640
│   └── 1.3.46.670589.11.10042.5.0.20936.2024030714034287428
│       ├── 1.3.46.670589.11.10042.5.0.6048.2024030714370454603
│       │   ├── 1.3.46.670589.11.10042.5.0.6048.2024030714374551656.dcm
│       │   ├── 1.3.46.670589.11.10042.5.0.6048.2024030714374554657.dcm
│       │   ├── 1.3.46.670589.11.10042.5.0.6048.2024030714374557658.dcm
│       │   ├── 1.3.46.670589.11.10042.5.0.6048.2024030714374562659.dcm
```

- Path

```
data/XNAT_Exxxxx/StudyInstanceUID/SeriesInstanceUID/SOPInstanceUID.dcm
```

3. label

> This folder contains metadata files and masks for each series.

```
label
├── XNAT_E09640
│   ├── SEG_20240529_222515_522_S1301_C_labels_metadata.csv
│   ├── SEG_20240529_222515_522_S1301.nii.gz
│   ├── SEG_20240529_222945_457_S1401_C_labels_metadata.csv
│   ├── SEG_20240529_222945_457_S1401.nii.gz
│   ├── SEG_20240529_223011_056_S1501_C_labels_metadata.csv
│   └── SEG_20240529_223011_056_S1501.nii.gz
```

- Mask File example

```python
import numpy as np

mask = ReadImage("/path/to/file.nii.gz")

np.unique(mask, return_counts=True)

# (array([0, 1, 2, 3], dtype=uint8), array([1326790,     308,       3,       3]))
```

In this example 👆, based on `labels_dictionary.json`, the DICOM series related to this mask is **Normal**.

> **Important Note**: There are pre-defined labels that exist in the mask array. In this example, pixel values **2** and **3** are pre-defined and can be ignored.