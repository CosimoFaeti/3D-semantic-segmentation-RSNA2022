<p align="center">
  <img src="https://github.com/user-attachments/assets/1b4d6d72-4b89-47d7-ac0a-f42f2f198774" alt="rsna-logo" width="30%">
</p>

# 3D Semantic Segmentation - RSNA 2022
---
The **[RSNA 2022 Cervical Spine Fracture Detection](https://www.kaggle.com/competitions/rsna-2022-cervical-spine-fracture-detection)** is organized by the Radiological Socity of North America (RSNA) along with the American Society of Neuroradiology (ASNR) and the American Society of Spine Radiology (ASSR). The ultimate goal of the challenge is to develop an AI system used to aid in the detection and localization of cervical spine fractures.

The training dataset provided is constituted by 2019 CT scans, with one folder for each scan, containing image data in dicom file format. Moreover, segmentation masks (pixel level annotations) are provided for a subset (87 scans) of the training set. The pixels assume values of 1 to 7 for C1 to C7 (seven cervical vertebrae) and 8 to 19 for T1 to T12. This data is provided in the nifti file format.

This repository contains the first task of the RSNA 2022 challenge, i.e., develop a 3D semantic segmentation model to assign segmentation masks to the unlabelled CT scans in the training data.

## Description
The project consists in four main steps which are briefly summarized as follows

1. **Data Preparation**: The data preparation phase includes multiple transformations performed over the CT scans and the segmentation masks. We resize CT scans, which differs in length, to a **target spatial size** ensuring that all inputs to the model have the same dimensions. In addition, we scale the intensity of each volume. We exploit many image augmentation techniques. For what concern the multi-class segmentation masks we apply **binary one-hot encoding**.

2. **Model Implementation**: The 3D segmentation model has **U-Net** architecture which is state-of-the-art for 3D segmentation of medical images. We exploit [MONAI](https://docs.monai.io/en/stable/networks.html#unet) library for its implementation.

3. **Model Training** The model has been trained using **AdamW** optimizer with learning rate scheduler. The loss function employed is the weighted sum of **Dice Loss** and **BCE (Binary Cross Entropy) Loss**.
```math
\text{Loss} = \alpha \cdot \text{BCE} + \beta \cdot \text{Dice Loss}
```
The model has been trained for 320 epochs.
<p align="center">
  <img src="https://github.com/user-attachments/assets/b70b36ba-8360-4a81-941e-175fc14a6084" alt="losses" width="50%">
  <img src="https://github.com/user-attachments/assets/2b5617d8-7eca-4d9c-801b-2c295628779d" alt="metric" width="50%">
</p>

4. **Prediction**


## Repository Overview
At the root level of this repository, you will find the code for exploratory data analysis, the training and prediction of the 3D semantic segmentation model, as well as files related to the model's configuration and results. More specifically:
* **[eda.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/eda.ipynb)**: This notebook contains an exploratory data analysis (EDA) of the dataset, including loading the data, visualizing images, and analyzing feature distributions;
* **[3d-semantic-segmentation.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/3d-semantic-segmentation.ipynb)**: This notebook documents the initial training process of the 3D U-Net model, including setting up the model architecture, defining training parameters, and running the first training iterations;
* **[3d-semantic-segmentation-resume-training.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/3d-semantic-segmentation-resume-training.ipynb)**: This notebook is used for resuming the training of the 3D U-Net model from a saved checkpoint, allowing the training process to continue given the GPU runtime limits imposed by the platform;
* **[3d-semantic-segmentation-prediction.ipynb](https://github.com/CosimoFaeti/3D-semantic-segmentation-RSNA2022/blob/main/3d-semantic-segmentation-prediction.ipynb)**: This notebook is dedicated to generating predictions using the trained 3D U-Net model on the test data, and evaluating the predictions through visualizations to assess model effectiveness.
* **[file]()**: This folder contains resulting files from the model training process:
  * **`HM8569LQ_losses_metrics_combined.csv`**: A CSV file with training and validation losses and metrics for all 320 epochs.
  * **`HM8659LQ_best_model`**: The best-performing model saved according to the evaluation metric.
  * **`HM8659LQ_config.pkl`**: A pickle file containing the configuration parameters used for the 3D U-Net model.

 
## Collaborators
---
* [Riccardo Galarducci](https://github.com/RiccardoGalarducci)
