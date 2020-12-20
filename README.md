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

```bash
conda activate mwcnn
```

## Dataset and data preprocessing

Step 1: Download training data (DIV2K HD images)
To download the dataset, use the command below:

```bash
cd data_gen
wget "http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_HR.zip"
unzip DIV2K_train_HR.zip .
```
or simply click [here](http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_HR.zip) and unzip it.

Step 2: Processing the images into patches:

Firstly, on Matlab, perform the following
```bash
cd data_gen #if not already in data_gen
```
Second, edit the path provided in 'A_data_generation.m' (line 12) to the location of the DIV2K dataset downloaded in step 1.
For example, "folder_train  = {'C:\Users\suhri\Desktop\ECE 251C\Project\DIV2K' };" in our case.

Third, run 'A_data_generation.m' and confirm that the patches are being generated.

Step 3: Downloading test data
You can use any test data of your choice.
Some popular datasets have been uploaded [here](https://drive.google.com/drive/folders/1HlIgV_l-RD-0bI5PTGj3F5VGWW7tZi1O?usp=sharing).


## Experiments performed

1) MWCNN vs DnCNN
	* Comparing the MWCNN model's performance under different noise levels with it's 'wavelet-less' counterpart

2) Effect of type and scale of noise
	* Checking if changing the type of noise (Gaussian / Poisson) or noise level (sigma 15, 30, 50) produces different results.

3) Effect of noise level and lighting conditions
	* Testing model's performance under different lighting conditions.

4) Effect of different wavelets
	* Using different wavelets - Haar, Symlet5, Daubechies5, Biorthogonal 2.4 to see if the denoising performance improves.

5) Cropped model vs New model
	* Creating a new model to accommodate the resized subband images of higher order filters.


## Training and Testing

### Training:

To train the model, run the following from the MWCNN environment.
```bash
python main.py --model MWCNN --save MWCNN_DeNoising --scale 15 --n_feats 64 --save_results --print_model --patch_size 256 --batch_size 4 --print_every 50 --lr 1.024e-4 --lr_decay 100 --n_colors 3 --save_models --task_type denoising --noise 'G'
```
* Change the scale (sigma value) to 15, 30 and 50 to reproduce the results we got for different noise levels.
* Change noise to 'G' for Gaussian noise and 'S' for Poisson noise.
* When using Haar Wavelet, use n_feats = 64. If using higher order filters, change number of features accordingly to accomodate the new sub-band image sizes.
* For Symlet5, Daubechies5 and Biorthogonal 2.4, we used n_feats = 66.


### Testing: 
* The pretrained models can be found [here](https://drive.google.com/drive/folders/1HlIgV_l-RD-0bI5PTGj3F5VGWW7tZi1O?usp=sharing).
* If you download the single channel weights, remember to change n_colors to 1 else use 3.

```bash
python main.py --model MWCNN --save MWCNN_DeNoising --scale 15 --n_feats 64 --save_results --print_model --n_colors 3 --test_only --resume -1 --pre_train pretrained_models/ --data_test Set5 --task_type denoising --noise 'G'
```

## Changes made

* To change the wavelet used,
go to 'MWCNNv2\MWCNN_code\model\common.py'

* Comment out lines 68-79 and uncomment lines 81-106.
* Comment out lines 134-153 and uncomment lines 110-130. Change the wavelet used based on the [pywavelets documentation](https://pywavelets.readthedocs.io/en/latest/).

## Results

1) MWCNN vs DnCNN

[](\images\mwcnnvsdncnn.png)
2) Effect of type and scale of noise

3) Effect of noise level and lighting conditions

4) Effect of different wavelets

5) Cropped model vs New model
