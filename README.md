# SRGANs : Spectral Regularization for Combating Mode Collapse in GANs
Image generation on ImageNet. 
Image generation on CIFAR-10 and STL-10 can be found: https://github.com/max-liu-112/SRGANs-Spectral-Regularization-GANs-
### References
-Kanglin Liu, Wenming Tang, Fei Zhou, Guoping Qiu. *Spectral Regularization for Combating Mode Collapse in GANs*. ICCV2019. [SRGANs]

* The implementation is Based on SNGANs https://github.com/pfnet-research/sngan_projection, 

* The setup and example code in this README are for training SRGANs on 4 GPUs.

## Setup

### Install required python libraries:
chainer==3.3.0

tensorflow-gpu==1.2.0

numpy==1.11.1

cython==0.27.2

cupy==2.0.0

scipy==0.19.0

pillow==4.3.0

pyyaml==3.12

h5py==2.7.1

### Experiment setup
please refer to SNGANs https://github.com/pfnet-research/sngan_projection

### Train the model

The defailt setting of Batch size is 2048. 
First, we train the model identical to SN-GANs. (No Spectral Regularization in involved)

`python train.py`

With such a setting, mode collapse begins at iteration=40k. 
Spectral Collapse is also observed and shown in the following figure.

<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/fig1_is.jpg">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/fig1=2_fid.pjpg">

Then we resume the training with the snapshot at iterations=40k. Now we apply proposed SR to model.
(trun the updater args 'apply_SR' in confgis/config.yaml to 'True')
We can see that applying SR avoid the mode collapse problem, and greatly improve the model performance.


### Spectral Collapse VS Mode Collapse
SNGAN: iterations=40k
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_40k_id204.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_40k_id265.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_40k_id323.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_40k_id946.png">
SNGAN: iterations=70k
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_70k_id204.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_70k_id265.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_70k_id323.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SNGAN_70k_id946.png">
SRGAN: iterations=70k
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SRGAN_40k_id204.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SRGAN_40k_id265.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SRGAN_40k_id323.png">
<img src="https://github.com/max-liu-112/SRGANs/blob/master/figures/SRGAN_40k_id946.png">


