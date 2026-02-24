# Prostate MRI Preprocessing & Visualization Pipeline

## Overview
This repository presents a Python-based workflow for **prostate MRI preprocessing and visualization**, focusing on accurate isolation and visualization of the **prostate region of interest (ROI)** from T2-weighted MRI scans.

The pipeline loads medical imaging data in NIfTI format, applies prostate gland segmentation masks, enhances image contrast within the ROI using CLAHE and gamma correction, and generates high-quality visual outputs with segmentation-based contour overlays. This work serves as a foundational step for radiomics analysis, machine learning, and imaging-based clinical research.

---

## Dataset
The dataset includes prostate MRI scans from multiple patients. For each patient, the following files are used:

- `*_t2w.nii.gz` – T2-weighted MRI volume  
- `*_gland.nii.gz` – Binary prostate gland segmentation mask  

All files are stored in NIfTI (`.nii.gz`) format and processed slice-wise.

**Note:** The MRI dataset is **not included in this repository** due to size and data governance considerations.

To run this project locally:

1. Create a `data/` directory in the project root.
2. Inside `data/`, create subfolders for each patient (e.g., `10005`, `10040`, etc.).
3. Place the corresponding:
   - `*_t2w.nii.gz`
   - `*_gland.nii.gz`
   files inside each patient folder.

---

## Tools & Libraries
- **Python**
- **SimpleITK** – medical image loading and volumetric data handling
- **OpenCV** – image masking, CLAHE contrast enhancement, gamma correction
- **NumPy** – numerical operations
- **Matplotlib** – visualization and image export

---

## Workflow

### Image Loading
MRI volumes and corresponding segmentation masks are loaded using SimpleITK and converted into NumPy arrays for slice-wise processing.

### Slice Selection
The middle axial slice of each MRI volume is selected to provide a representative anatomical cross-section of the prostate.

### Intensity Normalization
The selected T2-weighted slice is normalized to an 8-bit intensity range (0–255) for visualization.

### ROI Extraction
The segmentation mask is binarized and applied to the MRI slice using bitwise operations, isolating the prostate gland while suppressing surrounding tissue.

### Contrast Enhancement
To improve tissue visibility within the prostate region:

- Contrast Limited Adaptive Histogram Equalization (CLAHE) is applied  
- Gamma correction is performed to enhance soft-tissue contrast  

Enhancement operations are strictly restricted to the prostate ROI.

### Contour Overlay
The prostate boundary is visualized by drawing a contour directly from the segmentation mask and overlaying it on the original MRI slice. This validates spatial alignment between the MRI and segmentation.

### Visualization
For each patient, three visual panels are generated:

1. Original T2-weighted MRI slice  
2. Masked and enhanced prostate ROI  
3. Original MRI with prostate contour overlay  

### Export
Final figures are saved as high-resolution PNG images (`results/{patient_id}_final.png`) for documentation and research reporting.

---

## Outputs
The generated visualizations verify:

- Correct spatial alignment between MRI volumes and segmentation masks  
- Accurate extraction of the prostate region of interest  
- Clear delineation of prostate boundaries using mask-based contour overlays  

These validations are essential prior to quantitative imaging and radiomics analysis.

---

## Applications
This preprocessing framework can be extended to support:

- Radiomic feature extraction workflows  
- Feature heatmap visualization  
- Multi-sequence MRI integration (T2W, ADC, PSMA PET)  
- Machine learning and radiogenomics modeling  

---
