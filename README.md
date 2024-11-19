This project was developed for the necessity of seperating the ECG waveform from the background of scanned clinical ECG images. These images tend to have noise and artefacts present, affecting the ability of existing methods to perform waveform extraction. The need for waveform extraction is important as it allows (after digitisation) to input the data into time series-based models that have published high results. Additionally it will assist with poor performance of ECG classification tasks as it will remove the noisy, uneeded parts of the images. 

The data involved in this project is from 5 sources below:

Public data:
- Physionet (... images)

Clinical data:
- PRECISE (... images)
- Huawei (... images)
- L-HARP (... images)
- Guangzhou (... images)

  nnUNet was the framework used to train the segmentation model (https://github.com/MIC-DKFZ/nnUNet).

  1. Create a conda environment and install nnunet

```
# Create conda environment
conda create --name nnunet 

# Activate conda environment
source activate nnunet

# Install pytorch
pip install pytorch

# Install nnunet
pip install nnunetv2

```

2. Set environment variables

```
# Set environment variables
export nnUNet_raw="/media/fabian/nnUNet_raw"
export nnUNet_preprocessed="/media/fabian/nnUNet_preprocessed"
export nnUNet_results="/media/fabian/nnUNet_results"
```

3. Prepare dataset in nnunet format

https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_format.md

4. Verify dataset integrity and pre-process

```
nnUNetv2_plan_and_preprocess -d DATASET_ID --verify_dataset_integrity
```

5. Train dataset for each fold [0,1,2,3,4]

```
nnUNetv2_train DATASET_NAME_OR_ID UNET_CONFIGURATION FOLD
```

6. Make predictions on imagesTs

```
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_NAME_OR_ID -c CONFIGURATION --save_probabilities
```
