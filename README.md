# MAMA-MIAAI - Here we go again
## Release Notes
**Version 1.0.0**: Initial release. This release introduces the MAMA-MIAAI dataset, providing automatically generated breast tissue segmentation masks and corresponding N4 bias-corrected MRI scans for all 1,506 subjects from the original MAMA-MIA collection.

## Overview
This repository provides a curated dataset built upon the [MAMA-MIA](https://github.com/LidiaGarrucho/MAMA-MIA) collection, augmented with breast tissue segmentation masks and N4 Bias Field corrected images. Our goal is to facilitate reproducible research on breast imaging by supplying
- Automatically generated breast tissue segmentation masks
- N4 Bias Field corrected images using SimpleITK

## Original MAMA-MIA Dataset
The base data consists of four subdatasets collected in the MAMA-MIA dataset:
- **DUKE**: 291 subjects
- **ISPY1**: 171 subjects
- **ISPY2**: 980 subjects
- **NACT**: 64 subjects
For details on sample acquisition, imaging parameters and licensing, please refer to the original implementation:<br>
MAMA-MIA GitHub: https://github.com/LidiaGarrucho/MAMA-MIA

## Data Processing and Methodology
### Breast Tissue Segmentation
We applied our deep learning breast tissue segmentation model to the pre-contrast T1 scan of all subjects to generate binary masks. These masks successfully isolate the breast tissue regions from the background and other surrounding anatomical structures.

The code used to generate these masks, including the model weights, has been open-sourced as supplementary material and is available here: [https://github.com/FloXyPython/MRI_BreastSeg](https://github.com/FloXyPython/MRI_BreastSeg). All necessary information for understanding and utilizing the resulting dataset is documented directly within this repository.
### N4 Bias Field Correction & Relationship to Masks
To correct intensity nonuniformities caused by the MRI magnetic field, we performed N4 Bias Field correction on each image using the Python implementation of SimpleITK. 

**Relationship:** The automatically generated breast tissue segmentation masks are used directly as input weights/masks to guide the N4 Bias Field correction algorithm. By supplying these masks, the N4 algorithm calculates the bias field exclusively over the actual breast tissue rather than the entire field of view. This prevents background noise and irrelevant anatomy from skewing the correction, resulting in a highly accurate and localized intensity normalization.

More information on bias field correction and its impact on radiomics can be found in [^1] and [^2].

[^1]: Schwarzhans F, George G, Sanchez LE, Zaric O, Abraham JE, Woitek R, Hatamikia S. Image normalization techniques and their effect on the robustness and predictive power of breast MRI radiomics. European Journal of Radiology. 2025 Jun 1;187:112086.<br>
[^2]: Juntu J, Sijbers J, Van Dyck D, Gielen J. Bias field correction for MRI images. InComputer Recognition Systems: Proceedings of the 4th International Conference on Computer Recognition Systems CORES’05 2005 (pp. 543-551). Springer Berlin Heidelberg.<br>

## Dataset Structure, Naming Scheme, and Formats
The dataset contains data for a total of 1,506 subjects across the four subdatasets (DUKE: 291, ISPY1: 171, ISPY2: 980, NACT: 64). All imaging files and masks are provided in compressed NIfTI format (`.nii.gz`).

### Folder Structure
<pre>
MAMA-MIAAI/
├── README.md
├── BreastSegmentation/           # Total: 1,506 mask files
│   ├── DUKE001_segmentation.nii.gz
│   ├── DUKE002_segmentation.nii.gz
│   └── ...
└── BiasCorrection/               # Total: 1,506 subject folders
    ├── DUKE001/
    │   ├── Scan01_corrected.nii.gz
    │   ├── Scan02_corrected.nii.gz
    │   └── ...
    ├── DUKE002/
    │   └── ...
    └── ...
</pre>

### File Naming Scheme and Formats
- **Segmentation Masks:** Located in the `BreastSegmentation/` directory. Files are named following the `{Subject_ID}_segmentation.nii.gz` convention. These are binary masks where a value of `1` represents breast tissue and `0` represents the background.
- **Bias-Corrected Scans:** Located in the `BiasCorrection/` directory and nested by subject ID (`{Subject_ID}/`). The corrected MRI volumes are named using the `{Scan_ID}_corrected.nii.gz` convention. 
- **File Format:** All imaging data is distributed as `.nii.gz` files. These can be natively loaded using standard Python medical imaging libraries (e.g., `SimpleITK`, `nibabel`) or viewed in clinical research software such as ITK-SNAP or 3D Slicer.

The dataset is hosted on **Figshare** and available via https://doi.org/10.6084/m9.figshare.29488250.v1

## Citation
If you use this dataset in your work, please cite the following:<br>
For the original MAMA-MIA dataset:
#### BibTex:
````
@article{garrucho2025,
  title={A large-scale multicenter breast cancer DCE-MRI benchmark dataset with expert segmentations},
  author={Garrucho, Lidia and Kushibar, Kaisar and Reidel, Claire-Anne and Joshi, Smriti and Osuala, Richard and Tsirikoglou, Apostolia and Bobowicz, Maciej and Riego, Javier del and Catanese, Alessandro and Gwoździewicz, Katarzyna and Cosaka, Maria-Laura and Abo-Elhoda, Pasant M and Tantawy, Sara W and Sakrana, Shorouq S and Shawky-Abdelfatah, Norhan O and Salem, Amr Muhammad Abdo and Kozana, Androniki and Divjak, Eugen and Ivanac, Gordana and Nikiforaki, Katerina and Klontzas, Michail E and García-Dosdá, Rosa and Gulsun-Akpinar, Meltem and Lafcı, Oğuz and Mann, Ritse and Martín-Isla, Carlos and Prior, Fred and Marias, Kostas and Starmans, Martijn P A and Strand, Fredrik and Díaz, Oliver and Igual, Laura and Lekadir, Karim},
  journal = {Scientific Data},
  year = {2025},
  doi = {10.1038/s41597-025-04707-4},
  pages = {453},
  number = {1},
  volume = {12}
}
````
