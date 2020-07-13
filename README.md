# ML-GCN.pytorch
PyTorch implementation of [Multi-Label Image Recognition with Graph Convolutional Networks](https://arxiv.org/abs/1904.03582), CVPR 2019.

## Update
1. In our original conference paper, we report the baseline classification results using GAP for comparison, because GAP is the default choice for feature aggregation in ResNet series. In our experiments, we found that replacing GAP with GMP leads to improved performance, and thus adopt GMP with our GCN method. During the review process of our conference paper, we provided extensive ablation studies about GAP and GMP in the supplementary materials. However, because the usage of GMP is like a trick and lacks convincing explanation, we have not included the GMP results as well as the discussions about the GMP results in the camera-ready version after careful deliberation. We re-run the importance baselines and report the latest results in below table. 

| Method    | COCO    | NUS-WIDE |VOC2007  |
|:---------:|:-------:|:-------:|:--------:|
| Res-101 GAP  | 77.3    |   56.9   |  91.7|
| Res-101 GMP |  81.5  | 59.7   |  93.0 |
| Ours        |  83.0  | 62.8   |  94.0 |


2. We update the equation 8 into the following form.
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
$$\bm{A'}_{ij} = 
\begin{cases} 
(p / \sum_{\substack{i=1 \\ i \neq j}}^{C} \bm{A}_{ij}) \times \bm{A}_{ij},  & if (i \neq j) \\
1 - p, & if (i = j)
\end{cases}\,,$$




### Requirements
Please, install the following packages
- numpy
- torch-0.3.1
- torchnet
- torchvision-0.2.0
- tqdm

### Download pretrain models
checkpoint/coco ([GoogleDrive](https://drive.google.com/open?id=1ivLi1Rc-dCUmN1ProcMk76zxF1DSvlIk))

checkpoint/voc ([GoogleDrive](https://drive.google.com/open?id=1lhbmW5g-Mo9KgI07nmc1kwSbEnb6t-YA))

or

[Baidu](https://pan.baidu.com/s/17j3lTjMRmXvWHT86zhaaVA)

### Options
- `lr`: learning rate
- `lrp`: factor for learning rate of pretrained layers. The learning rate of the pretrained layers is `lr * lrp`
- `batch-size`: number of images per batch
- `image-size`: size of the image
- `epochs`: number of training epochs
- `evaluate`: evaluate model on validation set
- `resume`: path to checkpoint

### Demo VOC 2007
```sh
python3 demo_voc2007_gcn.py data/voc --image-size 448 --batch-size 32 -e --resume checkpoint/voc/voc_checkpoint.pth.tar
```

### Demo COCO 2014
```sh
python3 demo_coco_gcn.py data/coco --image-size 448 --batch-size 32 -e --resume checkpoint/coco/coco_checkpoint.pth.tar
```

## Citing this repository
If you find this code useful in your research, please consider citing us:

```
@inproceedings{ML-GCN_CVPR_2019,
author = {Zhao-Min Chen and Xiu-Shen Wei and Peng Wang and Yanwen Guo},
title = {{Multi-Label Image Recognition with Graph Convolutional Networks}},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
year = {2019}
}
```
## Reference
This project is based on https://github.com/durandtibo/wildcat.pytorch

## Tips
If you have any questions about our work, please do not hesitate to contact us by emails.
