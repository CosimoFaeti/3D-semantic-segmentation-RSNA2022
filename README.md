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

### 1. Data Preparation
The data preparation phase includes multiple transformations performed over the CT scans and the segmentation masks. We resize the CT scans, which differ in length, to a target spatial size, ensuring that all inputs have the same dimensions. Then, we scale the intensity of each volume and apply several image augmentation techniques. For the multi-class segmentation masks, we apply binary one-hot encoding.
### 2. Model Implementation 
The 3D segmentation model has U-Net architecture which is *state-of-the-art* for 3D segmentation of medical images. We exploit **[MONAI](https://monai.io/)**  library for its implementation. 
### 3. Model Training
The model has been trained using AdamW optimizer with learning rate scheduler. The loss function employed is given by the weighted combination of *Dice Loss* and *BCE (Binary Cross Entropy) Loss*  which has been shown to yields the best result in terms of segmentation, pixel-wise accuracy, generalization and adversarial attacks. $\alpha$ and $\beta$ parameter has been chosen during the model selection phase.

```math
\text{Loss} = \alpha \cdot \text{BCE} + \beta \cdot \text{Dice Loss}
```
We exploited two different set of parameters:
* Model BCE+DiceLoss: $`\alpha=0.05`$ and $`\beta = 0.95`$
* Model DiceLoss: $`\alpha=0.0`$ and $`\beta = 1.0`$

The model has been trained for 560 epochs. The figures below shows the losses behaviour during training (left) and the dice metrics used for model evaluation (right).

<p align="center">
  <img src="https://github.com/user-attachments/assets/58ebeab4-7a21-42ce-8529-6025464fd63f" alt="losses" width="45%">
  <img src="https://github.com/user-attachments/assets/1acbe3a8-fa20-4996-8fb2-649c1f39a5aa" alt="metric" width="45%">
</p>

### 4. Prediction
As last step we predict the segmentation masks for the unlabelled CT scans using the best trained model according to the model selection phase.

The figure below shows the predicted segmentation masks by the model BCE+DiceLoss for some slices of a CT scan.

<p align="center">
  <img src="https://github.com/user-attachments/assets/c84ea5a7-4490-48cd-9ad8-d643299a0d5c" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/745bcd39-62ca-4333-9f75-c73596372bf8" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/0144965d-8a78-475b-99f8-14014385e176" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/cfb1fb4e-3d02-408c-8006-8fd6fed117c8" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/2709988a-55d2-4e7a-b6ef-b2ff7784cd12" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/00422baa-8bb2-4a36-977e-f2b9d998c13a" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/48eb58cd-947f-4ffe-8efe-f821a034dcc1" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/be2aace6-8eb2-4f4d-9357-7bce80fa6b3b" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/2292ef31-176b-43d7-b40d-fd1ce5bb4429" alt="pred1" width="80%">
</p>

The figure below shows the predicted segmentation masks by the model DiceLoss for some slices of a CT scan.

<p align="center">
  <img src="https://github.com/user-attachments/assets/56e05f6d-fa32-40ca-a3dc-6341a2f65def" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/870cca64-b92d-4225-8b5f-3c26f86e68c3" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/5aaed607-e7a0-4559-bb01-044b380c0cf2" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/c2d77c29-392b-4d41-91b2-a14489f8aed1" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/2e6c5c89-c0de-4323-8f3e-0c3ab2642519" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/0e1ce0f7-81a9-4ec0-9dc2-9c861e0b29a2" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/7c5d7927-52ea-4445-9ae2-c74718dcd10f" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/db169a67-79ca-4191-9577-711e008dd5ab" alt="pred1" width="80%">
  <img src="https://github.com/user-attachments/assets/d23b60a1-dd73-40cc-b85a-30ec7e3fafc8" alt="pred1" width="80%">
</p>

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
