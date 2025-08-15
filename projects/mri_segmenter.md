---
layout: default
title: MRI Segmenter
permalink: /projects/mri_segmenter/
---

<head>
    <script src="/files/donut.js"></script>
    <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
</head>

# Segmenting MRI Density/Magnitude Scans with a Fully Convolutional Network (FCN) ResNet

This project can be found on my <a href="https://github.com/Coy-Z/FCNResNet_Segmentation/">GitHub</a>.

This sub-project explores segmenting MRI scans with the built in FCN_ResNet_101 in PyTorch. The application of this particular segmentation is to use the segmentation as a high quality first estimate for blood vessel boundaries, which will then be refined using an iterative solver. The refined boundaries will then be used as a prior for the Inverse Navier-Stokes Problem. See Prof Matthew Juniper's <a href="https://mpj1001.user.srcf.net/MJ_Flow_MRI.html">website</a> for more details on the full project.

## The FCN ResNet Architecture

A Fully Convolutional Network (FCN) is effectively a Convolutional Neural Network (CNN) without a fully connected layer at its output. In other words, whereas a CNN takes an image in and spits out an output which is different in shape (e.g. a vector of class logits or a single binary class), an FCN outputs something of the same shape as the input (e.g. N $\times$ H $\times$ W tensor for an N-channel H $\times$ W image input).

The term ResNet is an abbreviation of Residual Network. Simply speaking, a ResNet uses residual blocks, which employ skip connections to combine the input with the output of the block. This addresses the vanishing gradients problem (where backpropagated gradients become very small). Residual blocks and skip connections allow a ResNet to have very deep networks with many layers, e.g. the ResNet used in this project has 101 layers.

## Loss Function and Training Scheme

With regards to the loss functions, we use a combined Weighted Cross-Entropy and Focal-Tversky Loss to train the FCN. These choices of loss functions allow us to preferentially target accurate positive (foreground) prediction, since the training data tends to sparse (majority background).

The training scheme employs two-level patience, with a patience-base learning rate scheduler (reduces LR on plateau) and patience-based early stopping in training to prevent overfiting. Combined with an AdamW regularised optimiser, this leads to very good generalisation and performance.

## Data

One of the largest difficulties of this project is the lack of quality pre-segmented data. To overcome this, we use a level set method to generate artificial data. The process is described below:

1. Use analytical methods or pre-written packages to generate a seed SDF. In this repo, I have written classes for tubes and circles. New seed geometries can be used by parsing the new SDF into the utils.data_gen_utils.SDF_MRI base class initialization.
2. Generate a speed field and modulate it with random functions.
3. Apply the speed field to the seed SDFs to perturb the geometry, forming a new SDF.
4. Apply an activation to the SDF with noise for the magnitude replica.
5. Apply a np.where() method for the binary mask.

In step 4, we add a combination of Gaussian white noise and correlated noise (sampled from an untrained Gaussian Process), to give accurate-looking MRI data.

We reserve real segmented MRI data for the validation set.

![Aorta](/files/mri_segmenter/aorta.png)
*Figure 1: This is a slice of the Aorta density scan.*

![Carotid](/files/mri_segmenter/carotid.png)
*Figure 2: This is a slice of the Carotid density scan.*

![Artificial](/files/mri_segmenter/artificial_data.png)
*Figure 3: This is a slice of the artificially generated density scan. The white lines overlayed on the magnitude scan are Signed Distance Field contours.*

Note: The real MRI data is not yet publicly available.

## Running the repo

Clone the repo, then run
```python
pip install requirements.txt
```
and the install torch from the official PyTorch <a href="https://pytorch.org/get-started/locally/">website</a>.

The data folder should be formatted as:
```pgsql
data/
├── train/
|   ├── magn/
|   |   ├──train_file_name_1
|   |   ├──train_file_name_2
|   |   :
|   └── mask/
|       ├──train_file_name_1
|       ├──train_file_name_2
|       :
└── val/
    ├── magn/
    |   ├──val_file_name_1
    |   ├──val_file_name_2
    |   :
    └── mask/
        ├──val_file_name_1
        ├──val_file_name_2
        :
```

15/08/2025