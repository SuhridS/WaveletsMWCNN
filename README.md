# Wavelets_MWCNN
* This project focuses on experiments to prove or disprove the efficacy of the MWCNN (Multi Wavelet Convolutional Neural Network) architecture under different lighting conditions and multiple noise inputs.
* We also plan on tweaking the network architecture to see if changing the activation function, wavelet used or network depth and other hyperparameters can help improving the PSNR or speed of performance.
* The following sections would help provide a deeper insight into the experiments performed.



## File structure

```
.
│   environment_requirements.yml
│   LICENSE
│   README.md
│
├───data_gen
│   │   A_data_generation.m
│   │   patches_generation.m
│   │   stride_init.m
│   │
│   └───MWCNN
└───MWCNN_code
    │   dataloader.py
    │   main.py
    │   option.py
    │   template.py
    │   trainer.py
    │   utility.py
    │   __init__.py
    │
    ├───data
    │   │   benchmark.py
    │   │   common.py
    │   │   demo.py
    │   │   div2k.py
    │   │   srdata.py
    │   │   __init__.py   
    │
    ├───experiment
    ├───loss
    │   │   adversarial.py
    │   │   discriminator.py
    │   │   vgg.py
    │   │   __init__.py
    │   │
    │   └───__pycache__
    │           __init__.cpython-35.pyc
    │
    ├───model
    │   │   common.py
    │   │   mwcnn.py
    │   │   __init__.py
    │
    ├───pretrained_models
    └───tmp
```

## Creating the correct environment

Step 1: Cloning the repository

```bash
git clone https://github.com/SuhridS/Wavelets_MWCNN.git
```

Step 2: Setting the conda environment

```bash
conda env create -f environment_requirements.yml

```


## Dataset and data preprocessing

Step 1: Download training data (DIV2K HD images)
To download the dataset, use the command below:

```bash
cd data_gen
wget "http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_HR.zip"
```
or simply click [here](http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_HR.zip).

Step 2: Processing the images into patches:

Firstly, on Matlab, perform the following
```bash
cd data_gen #if not already in data_gen
```
Second, edit the path provided in 'A_data_generation.m' (line 12) to the location of the DIV2K dataset downloaded in step 1.

Third, run 'A_data_generation.m'

## Experiments performed



## Training and Testing


## Changes made


## Pretrained models


## Results
