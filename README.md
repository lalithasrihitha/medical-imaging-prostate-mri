# Prostate MRI Preprocessing & Visualization Pipeline

## Overview
This repository presents a Python-based workflow for **prostate MRI preprocessing and visualization**, focusing on accurate isolation and visualization of the **prostate region of interest (ROI)** from T2-weighted MRI scans.

The pipeline loads medical imaging data in NIfTI format, applies prostate gland segmentation masks, enhances image contrast within the ROI, and generates high-quality visual outputs. This work serves as a foundational step for radiomics analysis, machine learning, and imaging-based clinical research.

---

## Dataset
The dataset includes prostate MRI scans from multiple patients. For each patient, the following files are used:

- `*_t2w.nii.gz` – T2-weighted MRI volume  
- `*_gland.nii.gz` – Binary prostate gland segmentation mask  

All files are stored in NIfTI (`.nii.gz`) format and processed slice-wise.

---

## Tools & Libraries
- **Python**
- **SimpleITK** – medical image loading and processing
- **OpenCV** – image masking, CLAHE contrast enhancement, gamma correction
- **NumPy** – numerical operations
- **Matplotlib** – visualization and image export

---

## Workflow

### Image Loading
MRI volumes and corresponding segmentation masks are loaded using SimpleITK and converted into NumPy arrays for processing.

### Slice Selection
The middle axial slice of each MRI volume is selected to provide a representative anatomical view of the prostate.

### ROI Extraction
The segmentation mask is binarized and applied to the MRI slice using bitwise operations, isolating the prostate gland while suppressing background tissue.

### Contrast Enhancement
To improve tissue visibility within the prostate:
- Contrast Limited Adaptive Histogram Equalization (CLAHE) is applied
- Gamma correction is used to further enhance soft-tissue contrast
Enhancement operations are restricted strictly to the prostate ROI.

### Visualization
For each patient, three visual outputs are generated:
1. Original T2-weighted MRI slice  
2. Masked and enhanced prostate ROI  
3. Original MRI with prostate contour overlaid  

### Export
Final figures are saved as high-resolution PNG images suitable for documentation and research reporting.



## Outputs
The generated visualizations verify:
- Correct spatial alignment between MRI images and segmentation masks
- Accurate extraction of the prostate region of interest
- Clear delineation of prostate boundaries via contour overlays

These validations are essential prior to quantitative imaging and radiomics analysis.

---

## Applications
This pipeline can be extended to support:
- Radiomic feature extraction workflows
- Heatmap and voxel-wise feature visualization
- Multi-sequence MRI analysis (T2W, ADC, PSMA PET)
- Machine learning and radiogenomics modeling

---

