
<p align="center">
  <img height="250" width="250" src="https://github.com/RiccardoGalarducci/3D-semantic-segmentation-RSNA2022-kaggle/blob/main/images/thumbnail.png" hspace="40">
</p>


# 3D Semantic Segmentation - RSNA 2022

The **[RSNA 2022 Cervical Spine Fracture Detection](https://www.kaggle.com/competitions/rsna-2022-cervical-spine-fracture-detection)** is a kaggle competition organized by the Radiological Socity of North America (RSNA) along with the American Society of Neuroradiology (ASNR) and the American Society of Spine Radiology (ASSR).
The ultimate goal of the challenge is to develop an AI system used to aid in the detection and localization of cervical spine fractures.

The training dataset provided is constituted by 2019 CT scans of the cervical spine, with one folder for each scan, containing image data in dicom file format. In addition, segmentation masks (pixel level annotations) are provided for a subset (87 scans) of the training data. The pixels assume values of 1 to 7 for C1 to C7 (seven cervical vertebrae) and 8 to 19 for T1 to T12. This data is provided in the nifti file format. 

This repository contains the first task of the RSNA 2022 challenge, i.e., develop a 3D semantic segmentation model to segment the 1932 unlabelled CT scans in the training data.

## Description

The project is composed by four main steps which are briefly summarized below.

### 1. Data Preparation
The data preparation phase includes multiple transformations performed over the CT scans and the segmentation masks. We resize the CT scans, which differ in length, to a target spatial size, ensuring that all inputs have the same dimensions. Then, we scale the intensity of each volume and apply several image augmentation techniques. For the multi-class segmentation masks, we apply binary one-hot encoding.
### 2. Model Implementation 
The 3D segmentation model has U-Net architecture which is *state-of-the-art* for 3D segmentation of medical images. We exploit **[MONAI](https://monai.io/)**  library for its implementation. 
### 3. Model Training
The model has been trained using AdamW optimizer with learning rate scheduler. The loss function employed is given by the weighted combination of *Dice Loss* and *BCE (Binary Cross Entropy) Loss*  which has been shown to yields the best result in terms of segmentation, pixel-wise accuracy, generalization and adversarial attacks. $\alpha$ and $\beta$ parameter has been chosen during the model selection phase.

```math
\text{Loss} = \alpha \cdot \text{BCE} + \beta \cdot \text{Dice Loss}
```

We exploited two set of parameters:
* *Model BCE-DiceLoss*: $` \alpha = 0.05 `$ and $` \beta = 0.95 `$
* *Model DiceLoss*: $` \alpha = 0.0 `$ and $` \beta = 1.0 `$

The model DiceLoss has been trained for 560 epochs, while the model BCE-DiceLoss for 530 epochs. The figures below shows the losses behaviour during training (left) and the dice metrics used for model evaluation (right) (Model DiceLoss).

<p align="center">
  <img width="45%" src=https://github.com/user-attachments/assets/03030c9e-1260-4839-ac87-22058fa00b79
>
  <img width="45%" src=https://github.com/user-attachments/assets/3fa700a7-3bd8-4565-9c7b-1a0ca7e106d8
>
</p>

### 4. Prediction
As last step we predict the segmentation masks for the unlabelled CT scans using the best trained model according to the model selection phase.

The figure below shows the predicted segmentation masks by *model BCE-DiceLoss* for some slices of a CT scan.

<p align="center">
<img width="80%" src=https://github.com/user-attachments/assets/c84ea5a7-4490-48cd-9ad8-d643299a0d5c
>
<img width="80%" src=https://github.com/user-attachments/assets/745bcd39-62ca-4333-9f75-c73596372bf8
>
<img width="80%" src=https://github.com/user-attachments/assets/0144965d-8a78-475b-99f8-14014385e176
>
<img width="80%" src=https://github.com/user-attachments/assets/cfb1fb4e-3d02-408c-8006-8fd6fed117c8
>
<img width="80%" src=https://github.com/user-attachments/assets/2709988a-55d2-4e7a-b6ef-b2ff7784cd12
>
<img width="80%" src=https://github.com/user-attachments/assets/00422baa-8bb2-4a36-977e-f2b9d998c13a
>
<img width="80%" src=https://github.com/user-attachments/assets/48eb58cd-947f-4ffe-8efe-f821a034dcc1
>
<img width="80%" src=https://github.com/user-attachments/assets/be2aace6-8eb2-4f4d-9357-7bce80fa6b3b
>
<img width="80%" src=https://github.com/user-attachments/assets/2292ef31-176b-43d7-b40d-fd1ce5bb4429
>
</p>

The figure below shows the predicted segmentation masks by *model DiceLoss* for some slices of a CT scan.

<p align="center">
<img width="80%" src=https://github.com/user-attachments/assets/ee57f341-72cc-4fcf-b6b6-64e9bbb8e69f
>
<img width="80%" src=https://github.com/user-attachments/assets/f1f836c0-d321-4cf5-9052-09edfb339c1c
>
<img width="80%" src=https://github.com/user-attachments/assets/1a66da68-037b-4d77-9551-b2a70f4ec0ac
>
<img width="80%" src=https://github.com/user-attachments/assets/0192bf2e-cf25-4846-8b66-bf256b68f450
>
<img width="80%" src=https://github.com/user-attachments/assets/cfe53ebe-54fc-4ac7-a38c-1f9cdcf6a647
>
<img width="80%" src=https://github.com/user-attachments/assets/7472a779-b246-46a8-a5ca-997b3868d0ab
>
<img width="80%" src=https://github.com/user-attachments/assets/7629328f-88f4-429f-a3b7-3fb89d5a25a3
>
<img width="80%" src=https://github.com/user-attachments/assets/7488aab0-12fa-4353-9a0d-11ef42169a03
>
<img width="80%" src=https://github.com/user-attachments/assets/28e9a15f-4de7-4895-b16b-1332e2ffea4d
>
</p>



## Repository Overview
At the root level of this repository, you will find the jupyter notebook for the training and prediction of the 3D semantic segmentation model. More specifically:
* **[3d-semantic-segmentation.ipynb](https://github.com/RiccardoGalarducci/3D-semantic-segmentation-RSNA2022-kaggle/blob/main/3d-semantic-segmentation.ipynb)**: This notebook  contains the initial training process of the 3D U-Net model, including setting up the model architecture, defining training parameters, and running the first training iterations;
* **[3d-semantic-segmentation-resume-training.ipynb](https://github.com/RiccardoGalarducci/3D-semantic-segmentation-RSNA2022-kaggle/blob/main/3d-semantic-segmentation-resume-training.ipynb)**: This notebook is used for resuming the training of the 3D U-Net model from a saved checkpoint, allowing the training process to continue;
* **[3d-semantic-segmentation-prediction.ipynb](https://github.com/RiccardoGalarducci/3D-semantic-segmentation-RSNA2022-kaggle/blob/main/3d-semantic-segmentation-prediction.ipynb)**: This notebook is dedicated to generating predictions using the trained 3D U-Net model on the test data, and evaluating the predictions through visualizations to assess model effectiveness.


## Collaborators

* **[Cosimo Faeti](https://github.com/CosimoFaeti)**
