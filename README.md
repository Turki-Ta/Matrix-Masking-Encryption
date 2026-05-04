# Privacy-Preserving Machine Learning: Static Matrix Masking & Domain Generalization

## Abstract
This repository contains the official code for our **Left-Sided Matrix Masking** framework ($X' = AX$). This method is designed for privacy-preserving machine learning, allowing data owners (e.g., hospitals) to generate exactly one static mask per class batch with near-zero computational overhead. The encrypted dataset is sent to the Cloud for heavy training, followed by a low-resource Domain Adaptation phase ("Figshare Logic") at the local level.

## 1. Setup Instructions
To replicate our environment and run these notebooks, you will need Python 3.x and a CUDA-enabled GPU. 

First, clone this repository:

    git clone https://github.com/YOUR-USERNAME/Matrix-Masking-Encryption.git
    cd Matrix-Masking-Encryption

Next, install the exact dependencies required:

    pip install -r requirements.txt

## 2. Datasets
Reviewers do **not** need to manually download or format any data. All datasets used in this research are programmed to download and process automatically when the respective notebooks are run:

* **OrganAMNIST (28x28):** Downloaded automatically via the official `medmnist` Python API.
* **SVHN Format 1 (128x128):** Downloaded directly from Stanford's servers. Our code includes a custom Python HDF5 parser that automatically extracts, crops, and pads the bounding boxes from `digitStruct.mat`.
* **Figshare Brain MRI (256x256):** Downloaded and unzipped automatically via the Kaggle API. 


## 3. Main Results & Evaluation
Below is a summary of the domain generalization accuracy achieved by the hospital's local model after our minimal transfer learning logic. The "Masked Accuracy" represents the security constraint (how well the model performs when the data is obscured), while the "Final Raw Accuracy" represents the model's recovered performance on the raw, unmasked data.

| Dataset | Pre-Transfer Masked Accuracy | Post-Transfer Raw Accuracy |
| :--- | :--- | :--- |
| **OrganAMNIST** | 98.94% | 91.92% |
| **SVHN** | 95.44% | 91.48% |
| **Figshare MRI** | 99.00%* | 91.69% |

## 4. Running the Code (Reproducibility)
To perfectly reproduce the figures, overhead metrics, and accuracy tables from our paper, run the notebooks in the `notebooks/` directory from start to finish.

* **`notebooks/1_Potential_Attacks.ipynb`**: Contains the Cryptanalysis visualization and reconstruction attacks (PCA, FastICA, NMF, TV-ICA) confirming the mathematical robustness of the framework.
* **`notebooks/2_organamnist_Dataset_V3.ipynb`**: Contains the Cloud Training and low-VRAM Figshare Transfer Logic for the OrganAMNIST dataset.
* **`notebooks/3_Figshare_Brain_MRI_dataset_V3.ipynb`**: Contains the high-resolution (256x256) implementation, including the Inference Batch Size Evaluation logic.
* **`notebooks/4_Street_View_House_Numbers_(SVHN)V3.ipynb`**: Contains the SVHN Format 1 HDF5 parser, masking logic, and extreme VRAM scaling experiments (4096 Cloud batch size to 512 Local batch size).
