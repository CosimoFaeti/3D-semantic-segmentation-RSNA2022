<p align="center">
  <img src="https://github.com/user-attachments/assets/1b4d6d72-4b89-47d7-ac0a-f42f2f198774" alt="rsna-logo" width="50%">
</p>

# 3D Semantic Segmentation - RSNA 2022
---
The **[RSNA 2022 Cervical Spine Fracture Detection](https://www.kaggle.com/competitions/rsna-2022-cervical-spine-fracture-detection)** is organized by the Radiological Socity of North America (RSNA) along with the American Society of Neuroradiology (ASNR) and the American Society of Spine Radiology (ASSR). The ultimate goal of the challenge is to develop an AI system used to aid in the detection and localization of cervical spine fractures.

The training dataset provided is constituted by 2019 CT scans, with one folder for each scan, containing image data in dicom file format. Moreover, segmentation masks (pixel level annotations) are provided for a subset (87 scans) of the training set. The pixels assume values of 1 to 7 for C1 to C7 (seven cervical vertebrae) and 8 to 19 for T1 to T12. This data is provided in the nifti file format.

This repository contains the first task of the RSNA 2022 challenge, i.e., develop a 3D semantic segmentation model to assign segmentation masks to the unlabelled CT scan in the training data.

## Description

## Repository Overview
At the root level of this repository, you will find the code for exploratory data analysis, the training and prediction of the 3D semantic segmentation model, as well as files related to the model's configuration and results. More specifically:
* **[eda.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/eda.ipynb)**: This notebook contains a comprehensive exploratory data analysis (EDA) of the dataset, including loading the data, visualizing images, and analyzing feature distributions;
* **[3d-semantic-segmentation.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/3d-semantic-segmentation.ipynb)**: This notebook documents the initial training process of the 3D U-Net model, including setting up the model architecture, defining training parameters, and running the first training iterations;
* **[3d-semantic-segmentation-resume-training.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/3d-semantic-segmentation-resume-training.ipynb)**: This notebook is used for resuming the training of the 3D U-Net model from a saved checkpoint, allowing the training process to continue given the GPU runtime limits imposed by the platform;
* **[3d-semantic-segmentation-prediction.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/3d-semantic-segmentation-prediction.ipynb)**: This notebook is dedicated to generating predictions using the trained 3D U-Net model on the test data, and evaluating the predictions through visualizations to assess model effectiveness.
* **file** 

 
## Collaborators
---
* [Riccardo Galarducci](https://github.com/RiccardoGalarducci)






Pre-processing

CausalInference_preprocessing.ipynb : contains the pre-processing step
Interrupted Time Series model:

CausalInference_ITS.ipynb : contains the implementation of ITS model (Ordinary Least Squares, OLS)
Bayesian Structural Time Series model:

CausalInference_BSTS_1.ipynb : contains the implementation of BSTS model (Maximum Likelihood Estimation, MLE)
CausalInference_BSTS_2.ipynb : contains the implementation of BSTS model (Variational Inference, VI)
CausalInference_BSTS_3.ipynb : contains the implementation of BSTS model (Hamiltonian Monte Carlo, HMC)
Inference analysis:

Inference_FINAL.ipynb : contains the inference analysis
