# SimulAI: Complete Deep Computer-Vision Methodology for Investigating Hydrodynamic Instabilities
This repository contains the official source code used to produce the results reported in the following papers:
[ourpaper]
All models, images and data can be found in this URL: https://drive.google.com/drive/folders/1OlS5ZuTunQlkYFN0bHJczLQoNC_Gqcgr.
If you use this code, please cite one of those papers (the first one when you work with hierarchy-based semantic embeddings, the second one when you use the cosine loss for classification).
The remainder of this ReadME will contain explanation on the work, database, source codes. Whilst each folder will contain how to run the specific model.



<details><summary><strong>Table of Contents</strong></summary>

1. [Rayleigh-Taylor Instability and Significance](#1-rayleigh-taylor-instability-and-significance)
2. [RayleAI - RTI Database](#2-rayleai-rti-database)
3. [LIRE](#3-lire)
4. [QATM](#4-qatm)
5. [InfoGAN](#5-infogan)
6. [pReg](#5-pReg)
7. [PredRNN](#5-predrnn)

</details>


## 1. Rayleigh-Taylor Instability and Significance

In fluid dynamics, one of the most important research fields is hydrodynamic instabilities and their evolution in different flow regimes. The investigation of said instabilities is concerned with the highly non-linear dynamics. Currently, three main methods are used for the understanding of such phenomenon - namely analytical models, experiments and simulations - and all of them are primarily investigated and correlated using human expertise. In this work we claim and demonstrate that a major portion of this research effort could and should be analysed using recent breakthrough advancements in the field of Computer Vision with Deep Learning (CVDL or Deep Computer-Vision). Specifically, we target and evaluate specific state-of-the-art techniques - such as Image Retrieval, Template Matching, Parameters Regression and Spatiotemporal Prediction - for the quantitative and qualitative benefits they provide. In order to do so we focus in this research on one of the most representative instabilities, the Rayleigh-Taylor one, simulate its behaviour and create an open-sourced state-of-the-art annotated database RayleAI. Finally, we use adjusted experimental results and novel physical loss methodologies to validate the correspondence of the predicted results to actual physical reality to prove the models correctness.
The techniques which were developed and proved in this work can be served as essential tools for physicists in the field of hydrodynamics for investigating a variety of physical systems, and also could be used via Transfer Learning to other instabilities research. A part of the techniques can be easily applied on already exist simulation results.

![Rayleigh-Taylor Instability](https://user-images.githubusercontent.com/27349725/78000356-d2cb6b00-733c-11ea-831d-0a9b5342673a.jpg)


## 2. RayleAI Database
The first model is the state-of-the-art database - RayleAI can be found and downloaded here https://drive.google.com/drive/folders/1OlS5ZuTunQlkYFN0bHJczLQoNC_Gqcgr. The database contains thresholded images from a simulation of a simple single-mode RTI perturbation with a resolution of 64x128 cells, 2.7cm in x axis and 5.4cm in y axis, while each fluid follows the equation of state of an ideal gas. The simulation input consists of three free parameters: Atwood number, gravity and the amplitude of the perturbation. The database contains of 101,250 images produced by 1350 different simulations (75 frames each) with unique pair of the free parameters. The format of the repository is built upon directories, each represents a simulation execution with the directory name indicating the parameters of the execution.
| Parameter | From | To  | Stride |           
|---------- | ---- | --- | ------ |
| Atwood    | 0.02 | 0.5 | 0.02   | 
| Gravity   | 600  | 800 | 25     |
| Amplitude | 0.1  | 0.5 | 0.1    |
| X         | 2.7  | 2.7 | 0      |
| Y         | 5.4  | 5.4 | 0      |


## 3. LIRE

LIRE is a library that provides a way to retrieve images from databases based on color and texture characteristics among other classic features. LIRE creates a \textit{Lucene} index of image features using both local and global methods. For the evaluation of the similarity of two images, one can calculate their distance in the space they were indexed to. Many state-of-the-art methods for extracting features can be used, such as Gabor Texture Features \cite{zhang2000content}, Tamura Features \cite{tamurafeatures}, or FCTH \cite{chatzichristofis2008fcth}. For our purposes, we found that the Tamura Features method is better than the other methods that LIRE provides as it indexes \textit{RayleAI} images in a more dispersed fashion. The Tamura feature vector of an image is an 18 double values descriptor that represents texture features in the image that correspond to human visual perception.

## 4. QATM
One variation of the Template Matching problem is defined as follows: Given an exemplar image $T$, find the most similar region of interest in a target image $S$ \cite{brunelli2009template}. Classic template matching methods often use Sum-of-Squared Differences (SSD) or Normalized Cross-Correlation (NCC) to asses the similarity score between a template and an underlying image. These approaches work well when the transformation between the template and the target search image is simple. However, with non-rigid transformations, which are common in real-life, they start to fail. Quality-Aware Template Matching (QATM) \cite{qatm} method is a standalone template matching algorithm and a trainable layer with trainable parameters that can be used in a Deep Neural Network. QATM is inspired by assessing the matching quality of the source and target templates. It defines the $QATM(t,s)$-measure as the product of likelihoods that a patch $s$ in $S$ is matched in $T$ and a patch $t$ in $T$ is matched in $S$. Once $QATM(t, s)$ is computed, we can compute the template matching map for the template image $T$ and the target search image $S$. Eventually, we can find the best-matched region ${R^*}$ which maximizes the overall matching quality. Therefore, the technique is of great need when templates are complicated and targets are noisy. Thus most suitable for RTI images from simulations and experiments.  

## 5. InfoGAN

The following values can be specified for `--dataset`:

- **CIFAR-10**: Interface to the [CIFAR-10][3] dataset with 10 classes.
- **CIFAR-100**: Interface to the [CIFAR-100][3] dataset with 100 classes.
- **CIFAR-100-a**: The first 50 classes of [CIFAR-100][3].
- **CIFAR-100-b**: The second 50 classes of [CIFAR-100][3].
- **CIFAR-100-b-consec**: The second 50 classes of [CIFAR-100][3], but numbered from 0-49 instead of 50-99.
- **ILSVRC**: Interface to the [ILSVRC 2012][4] dataset.
- **NAB**: Interface to the [NABirds][5] dataset, expecting images in the sub-directory `images`.
- **NAB-large**: The NABirds dataset with the default image size being twice as large (512 pixels instead of 256, cropped to 448x448).
- **CUB**: Interface to the [Caltech-UCSD Birds][22] dataset, expecting images in the sub-directory `images`. Despite the lack of any suffix, this dataset interface is equivalent to `NAB-large`, just with the CUB data. That means, the input image size is 448x448.
- **Cars**: Interface to the [Stanford Cars][29] dataset with an input image size of 448x448.
- **Flowers**: Interface to the [Oxford Flowers-102][30] dataset with an input image size of 448x448.
- **iNat** / **iNat2018**: Interface to the [iNaturalist 2018][31] dataset with 224x224 crops from images resized to 256 pixels. An underscore followed by the name of a super-category might be appended to restrict the dataset to that supercategory (e.g., "iNat_Aves").
- **iNat-large**: Like iNat but with the default image size being twice as large (512 pixels instead of 256, cropped to 448x448). For restricting the dataset to a certain super-category, append its name before the "-large" suffix (e.g., "iNat_Aves-large").
- **iNat2019** and **iNat2019-large**: Same as above but for the [2019 edition][32] of the iNaturalist challenge. As opposed to the previous edition, this one does not support restricting the dataset to super-classes.

To all datasets except CIFAR, one of the following suffixes may be appended:

- `-ilsvrcmean`: use mean and standard deviation from the ILSVRC dataset for pre-processing.
- `-caffe`: Caffe-style pre-processing (i.e., BGR channel ordering and no normalization of standard deviation).

For ILSVRC, you need to move the test images into sub-directories for each class. [This script][6] could be used for this, for example.

Own dataset interfaces can be defined by creating a new module in the [`datasets`](datasets/) package, defining a class derived from [`FileDatasetGenerator`](datasets/common.py), importing it in [`datasets/__init__.py`](datasets/__init__.py), and adding a branch for it in the `get_data_generator` function defined there.

### 2.5. Available network architectures

#### 2.5.1. Tested

For CIFAR:

- **simple**: The [Plain-11][7] architecture, a strictly sequential, shallow CNN with 11 trainable layers. Good for conducting quick experiments.
  For training this network architecture, we used `--max_decay 0.1` in addition to the other arguments provided above for the ResNet.
  This causes a continuous decay of the learning rate so that the final learning rate will be 10 times less than the initial one.
- **resnet-110**: The standard [ResNet-110][8].
- **resnet-110-fc**: Like `resnet-110`, but always with a fully-connected layer after the global average pooling, even when used for learning embeddings.
- **resnet-110-wfc**: A variant of `resnet-110-fc` with twice the number of channels per block.
- **wrn-28-10**: A [Wide Residual Network][9] with depth 28 and width 10.
- **pyramidnet-272-200**: A [Deep Pyramidal Residual Network][10]. Provides better performance than ResNet, but is also much slower.

For ImageNet and NABirds:

- **resnet-50**: The standard [ResNet-50][8] implementation from `keras-applications`.

#### 2.5.2. Experimental

For CIFAR:

- **resnet-32**: The standard [ResNet-32][8].
- **densenet-100-12**: A [Densely Connected Convolutional Network][12] with depth 100 and growth-rate 12.
- **densenet-100-24**: A [Densely Connected Convolutional Network][12] with depth 100 and growth-rate 24.
- **densenet-bc-190-40**: A [Densely Connected Convolutional Network][12] with bottleneck blocks and compression (depth 190 and growth-rate 40).

For ImageNet and NABirds:

- **resnet-101** and **resnet-152**: The standard implementaions of [ResNet-101 and ResNet-152][8] introduced in `keras-applications >= 1.0.7`.
- **rn18**, **rn34**, **rn50**, **rn101**, **rn152**, **rn200**: [ResNets][8] with different depths.
  Requires the [keras-resnet][13] package, but be aware that batch normalization is broken in version 0.1.0.
  Thus, you need to either use an earlier or later version or merge [this pull request][14].
- **nasnet-a**: The [NasNet-A][15] implementation from `keras-applications`.


### 2.6. Learning semantic embeddings for ILSVRC and NABirds

The previous sections have shown in detail how to learn semantic image embeddings for CIFAR-100.
In the following, we provide the calls to [learn_image_embeddings.py](learn_image_embeddings.py) that we used to train our semantic embedding models (including classification objective) on the [ILSVRC 2012][4] and [NABirds][5] datasets.

```shell
# ILSVRC
python learn_image_embeddings.py \
    --dataset ILSVRC \
    --data_root /path/to/imagenet/ \
    --embedding embeddings/imagenet_mintree.unitsphere.pickle \
    --architecture resnet-50 \
    --loss inv_corr \
    --cls_weight 0.1 \
    --lr_schedule SGDR \
    --sgdr_base_len 80 \
    --epochs 80 \
    --max_decay 0 \
    --batch_size 128 \
    --gpus 2 \
    --model_dump imagenet_unitsphere-embed+cls_rn50.model.h5

# NAB (from scratch)
python learn_image_embeddings.py \
    --dataset NAB \
    --data_root /path/to/nab/ \
    --embedding embeddings/nab.unitsphere.pickle \
    --architecture resnet-50 \
    --loss inv_corr \
    --cls_weight 0.1 \
    --lr_schedule SGDR \
    --sgdr_max_lr 0.5 \
    --max_decay 0 \
    --epochs 180 \
    --batch_size 128 \
    --gpus 2 \
    --read_workers 10 \
    --queue_size 20 \
    --model_dump nab_unitsphere-embed+cls_rn50.model.h5

# NAB (fine-tuned)
python learn_image_embeddings.py \
    --dataset NAB-ilsvrcmean \
    --data_root /path/to/nab/ \
    --embedding embeddings/nab.unitsphere.pickle \
    --architecture resnet-50 \
    --loss inv_corr \
    --cls_weight 0.1 \
    --finetune imagenet_unitsphere-embed+cls_rn50.model.h5 \
    --finetune_init 8 \
    --lr_schedule SGDR \
    --sgd_lr 0.1 \
    --sgdr_max_lr 0.5 \
    --max_decay 0 \
    --epochs 180 \
    --batch_size 128 \
    --gpus 2 \
    --read_workers 10 \
    --queue_size 20 \
    --model_dump nab_unitsphere-embed+cls_rn50_finetuned.model.h5
```

## 3. Requirements

- Python >= 3.5
- numpy
- numexpr
- keras >= 2.2.0
- tensorflow (we used v1.8)
- sklearn
- scipy
- pillow
- matplotlib


## 4. Pre-trained models

### 4.1. Download links

|  Dataset  |              Model              | Input Size | mAHP@250 | Balanced Accuracy |
|-----------|---------------------------------|:----------:|---------:|------------------:|
| CIFAR-100 | [Plain-11][16]                  |    32x32   |   82.05% |            74.10% |
| CIFAR-100 | [ResNet-110-wfc][17]            |    32x32   |   83.29% |            76.60% |
| CIFAR-100 | [PyramidNet-272-200][18]        |    32x32   |   86.38% |            80.49% |
| NABirds   | [ResNet-50 (from scratch)][19]  |   224x224  |   73.99% |            59.46% |
| NABirds   | [ResNet-50 (fine-tuned)][20]    |   224x224  |   81.46% |            69.49% |
| NABirds   | [ResNet-50 (from scratch)][27]  |   448x448  |   82.33% |            70.43% |
| NABirds   | [ResNet-50 (fine-tuned)][28]    |   448x448  |   88.11% |            76.79% |
| CUB       | [ResNet-50 (from scratch)][25]  |   448x448  |   83.33% |            70.14% |
| CUB       | [ResNet-50 (fine-tuned)][26]    |   448x448  |   92.24% |            80.23% |
| ILSVRC    | [ResNet-50][21] *               |   224x224  |   83.15% |            70.42% |

<p style="font-size: 0.8em">
* This is an updated model with slightly better performance than reported in the paper (~1 percent point).
The original model can be obtained <a href="https://github.com/cvjena/semantic-embeddings/releases/download/v1.0.0/imagenet_unitsphere-embed+cls_rn50.model.h5">here</a>.
</p>

### 4.2. Pre-processing

The pre-trained models provided above assume input images to be given in RGB color format and standardized by subtracting a dataset-specific channel-wise mean and dividing by a dataset-specific standard deviation.
The means and standard deviations for each dataset are provided in the following table.

|            Dataset          |                     Mean                     |            Standard Deviation            |
|-----------------------------|----------------------------------------------|------------------------------------------|
| CIFAR-100                   | `[129.30386353, 124.06987, 112.43356323]`    | `[68.17019653, 65.39176178, 70.4180603]` |
| NABirds (from scratch)      | `[125.30513277, 129.66606421, 118.45121113]` | `[57.0045467, 56.70059436, 68.44430446]` |
| CUB (from scratch)          | `[123.82988033, 127.35116805, 110.25606303]` | `[59.2230949, 58.0736071, 67.80251684]`  |
| ILSVRC & fine-tuned models  | `[122.65435242, 116.6545058, 103.99789959]`  | `[71.40583196, 69.56888997, 73.0440314]` |

### 4.3. Troubleshooting

Sometimes, loading of the pre-trained models fails with the error message "unknown opcode".
In the case of this or other issues, you can still create the architecture yourself and load the pre-trained weights from the model files provided above.
For CIFAR-100 and the `resnet-110-wfc` architecture, for example, this can be done as follows:

```python
import keras
import utils
from learn_image_embeddings import cls_model

model = utils.build_network(100, 'resnet-110-wfc')
model = keras.models.Model(
    model.inputs,
    keras.layers.Lambda(utils.l2norm, name = 'l2norm')(model.output)
)
model = cls_model(model, 100)

model.load_weights('cifar_unitsphere-embed+cls_resnet-110-wfc.model.h5')
```


[1]: https://arxiv.org/pdf/1809.09924
[2]: https://www.cs.toronto.edu/~kriz/cifar-100-python.tar.gz
[3]: https://www.cs.toronto.edu/~kriz/cifar.html
[4]: http://image-net.org/challenges/LSVRC/2012/
[5]: http://dl.allaboutbirds.org/nabirds
[6]: https://raw.githubusercontent.com/soumith/imagenetloader.torch/master/valprep.sh
[7]: http://hera.inf-cv.uni-jena.de:6680/pdf/Barz18:GoodTraining
[8]: https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/He_Deep_Residual_Learning_CVPR_2016_paper.pdf
[9]: https://arxiv.org/pdf/1605.07146.pdf
[10]: https://ieeexplore.ieee.org/abstract/document/8100151
[11]: https://arxiv.org/pdf/1409.1556.pdf
[12]: http://openaccess.thecvf.com/content_cvpr_2017/papers/Huang_Densely_Connected_Convolutional_CVPR_2017_paper.pdf
[13]: https://github.com/broadinstitute/keras-resnet
[14]: https://github.com/broadinstitute/keras-resnet/pull/47
[15]: https://arxiv.org/pdf/1707.07012.pdf
[16]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.0.0/cifar_unitsphere-embed+cls_plain11.model.h5
[17]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.0.0/cifar_unitsphere-embed+cls_resnet-110-fc.model.h5
[18]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.0.0/cifar_unitsphere-embed+cls_pyramidnet-272-200.model.h5
[19]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.0.0/nab_unitsphere-embed+cls_rn50.model.h5
[20]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.0.0/nab_unitsphere-embed+cls_rn50_finetuned.model.h5
[21]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.1.0/imagenet_unitsphere-embed+cls_rn50.model.h5
[22]: http://www.vision.caltech.edu/visipedia/CUB-200-2011.html
[23]: https://arxiv.org/pdf/1901.09054
[24]: CosineLoss.md
[25]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.1.0/cub_unitsphere-embed+cls_deep-hierarchy_rn50.model.h5
[26]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.1.0/cub_unitsphere-embed+cls_deep-hierarchy_rn50_finetuned.model.h5
[27]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.1.0/nab-large_unitsphere-embed+cls_rn50.model.h5
[28]: https://github.com/cvjena/semantic-embeddings/releases/download/v1.1.0/nab-large_unitsphere-embed+cls_rn50_finetuned.model.h5
[29]: https://ai.stanford.edu/~jkrause/cars/car_dataset.html
[30]: http://www.robots.ox.ac.uk/~vgg/data/flowers/102/index.html
[31]: https://github.com/visipedia/inat_comp/tree/2018
[32]: https://www.kaggle.com/c/inaturalist-2019-fgvc6/
