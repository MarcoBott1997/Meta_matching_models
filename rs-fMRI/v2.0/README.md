# Meta_matching_models v2.0 (Multilayer Meta-matching)
This folder contains v2.0 (multilayer meta-matching) models trained from 5 source datasets (UK Biobank, ABCD, GSP, HBN, eNKI-RS) and example to run it. This repo contains pre-trained Meta-matching models. If you want to train your own multilayer meta-matching models from scratch or view more details, please visit our [CBIG repo](https://github.com/ThomasYeoLab/CBIG/tree/master/stable_projects/predict_phenotypes/Chen2024_MMM).


## Reference
+ Chen, P., An, L., Wulan, N., Zhang, C., Zhang, S., Ooi, L. Q. R., ... & Yeo, B. T. (2023). [**Multilayer meta-matching: translating phenotypic prediction models from multiple datasets to small data**](https://www.biorxiv.org/content/10.1101/2023.12.05.569848v1.abstract). bioRxiv, 2023-12.

## Data Processing
Meta-matching model v2.0 used Schaefer2018 parcellation with 400 parcels and 19 sub-cortical regions. In order to use the pre-trained model, you need generate your own data with same parcellation. You can refer to the [data processing code for HCP dataset in our full release](https://github.com/ThomasYeoLab/CBIG/tree/master/stable_projects/predict_phenotypes/He2022_MM/data_processing#step-51-step-5-for-whole-data-processing-code) where we convert ICA FIX HCP S1200 data into 419 by 419 FC (functional connectivity) matrix with [Schaefer2016_400Parcels_17Networks_colors_19_09_16_subcortical.dlabel.nii](https://github.com/ThomasYeoLab/CBIG/blob/master/stable_projects/predict_phenotypes/He2022_MM/data_processing/step5_hcp_data/extra/Schaefer2016_400Parcels_17Networks_colors_19_09_16_subcortical.dlabel.nii), and [data processing code for UK Biobank dataset in our full release](https://github.com/ThomasYeoLab/CBIG/tree/master/stable_projects/predict_phenotypes/He2022_MM/data_processing#step-60-optional) where we convert rsfMRI data [data-field 20227 of UK Biobank](https://biobank.ctsu.ox.ac.uk/crystal/field.cgi?id=20227) to MNI152 2mm space then to 419 by 419 FC (functional connectivity) matrix with [Schaefer2018_400Parcels_17Networks_order_FSLMNI152_2mm.nii.gz](https://github.com/ThomasYeoLab/CBIG/blob/master/stable_projects/predict_phenotypes/He2022_MM/data_processing/step6_experiment_2/ukbb_20227_to_fc419/extra/Schaefer2018_400Parcels_17Networks_order_FSLMNI152_2mm.nii.gz). If you need more information about 19 sub-cortical regions, you can take a better look at [code that we created 419 mask for UK Biobank dataset in our full release](https://github.com/ThomasYeoLab/CBIG/blob/master/stable_projects/predict_phenotypes/He2022_MM/data_processing/step6_experiment_2/ukbb_20227_to_fc419/CBIG_MM_create_FC419_MNI2mm.m).

The model needs flatten FC for input, here is the simple code to flatten 419 by 419 matrix.
```python
import numpy as np
roi = 419
index = np.tril(np.ones(roi), k=-1) == 1
fc_flat = fc[index]
```
## Source phenotypes in each source dataset
The description of different source phenotypes can be found in Supplementary Tables 2 - 6 of Chen et al., 2023. 

## Usage
Please check meta_matching_v2.0.ipynb for the model usage and example.

## Bugs and Questions
Please contact Pansheng Chen at chenpansheng@gmail.com, Lijun An at anlijun.cn@gmail.com, Chen Zhang at chenzhangsutd@gmail.com and Thomas Yeo at yeoyeo02@gmail.com.
