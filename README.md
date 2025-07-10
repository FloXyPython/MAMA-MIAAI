# MAMA-MIAAI - Here we go again

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

## Our Extensions
### Breast Tissue Segmentation
We applied our own breast tissue segmentation model to the pre-contrast T1 scan of all subjects to generate binary masks identifying breast tissue regions.<br>
The code, including the model weights, has been open sourced and is available [here](https://github.com/FloXyPython/MRI_BreastSeg)

### N4 Bias Field Correction
To correct intensity nonuniformities, we performed N4 Bias Field correction on each image using SimpleITKs Python implementation, guided by the segmentation masks.<br>
More information on bias filed correction can be found in [^1] and [^2].

[^1]: Schwarzhans F, George G, Sanchez LE, Zaric O, Abraham JE, Woitek R, Hatamikia S. Image normalization techniques and their effect on the robustness and predictive power of breast MRI radiomics. European Journal of Radiology. 2025 Jun 1;187:112086.<br>
[^2]: Juntu J, Sijbers J, Van Dyck D, Gielen J. Bias field correction for MRI images. InComputer Recognition Systems: Proceedings of the 4th International Conference on Computer Recognition Systems CORES’05 2005 (pp. 543-551). Springer Berlin Heidelberg.<br>

## Data Access
<pre>
MAMA-MIAAI
├── readme.txt
├── BreastSegmentation
│   ├── DUKE001_segmentation
│   ├── DUKE002_segmentation
│   └── …
└── BiasCorrection
    ├── DUKE001
    │   ├── Scan01
    │   ├── Scan02
    │   └── …
    └── DUKE002
        ├── Scan01
        ├── Scan02
        └── …
</pre>

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
For this dataset:
#### BibTex:
````
@article{Schwarzhans2025,
  title={MAMA-MIAAI - Here we go again},
  author={Schwarzhans, Florian and Handa, Palak and Woitek, Ramona},
  year={2025},
  month={7},
  url={https://figshare.com/articles/dataset/MAMA-MIAAI_-_Here_we_go_again/29488250},
  doi={10.6084/m9.figshare.29488250.v1}
}
````
