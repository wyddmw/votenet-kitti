# votenet-kitti

## Introduction

This repository is the [VoteNet](https://arxiv.org/pdf/1904.09664.pdf) code implementation on KITTI Benchmark. The main parts of the code, including the network and loss computing，are changed from the [offical code release of the VoteNet](https://github.com/facebookresearch/votenet). The dataset and data augmentation part is changed from [PointRCNN offcial code release](https://github.com/sshaoshuai/PointRCNN). Comapred with VoteNet offical code release, the main changes are the codes in "kitti" folder.

## Installation

Install Pytorch and Tensorflow (for TensorBoard). It is required that you have access to GPUs. Matlab is required to prepare data for SUN RGB-D. The code is tested with Ubuntu 16.04, Pytorch v1.0, CUDA 10.0

Note in offical VoteNet: there is some incompatibility with newer version of Pytorch (e.g. v1.3), which is to be fixed.

And the installation details can be found in [official VoteNet code](https://github.com/facebookresearch/votenet).

As officially mentioned in VoteNet implementation, the following dependence is required:

```matplotlib
opencv-python
plyfile
'trimesh>=2.35.39,<2.35.40'
'networkx>=2.2,<2.3'
```

## Dataset preparation

The dataset preparation details can be found in [official PointRCNN code](https://github.com/sshaoshuai/PointRCNN).

Fisrt, please download the official KITTI 3D object detection dataset and organize the downloaded files as illustrated in PointRCNN.

Then, to use the ground truth sampling data augmentation for training, please generate the ground truth database as follows:

    cd kitti
	python generate_gt_database.py

## Training and evaluating

To train a new VoteNet model on KITTI data:
	python train.py --dataset sunrgbd --log_dir log_sunrgbd

To test the trained model with its checkpoint:
	python eval.py --dataset sunrgbd --checkpoint_path log_sunrgbd/checkpoint.tar --dump_dir eval_sunrgbd --cluster_sampling seed_fps --use_3d_nms --use_cls_nms --per_class_proposal

The details can be found in [VoteNet official code release](https://arxiv.org/pdf/1904.09664.pdf)

## Visualization

I have added some visualization codes in kitti_vote_dataset.py, which are commented out for the convenience of training. And the visualizations are as follows:

This is the visualization of points and 3D boxes in one augmentated scene.
![teaser](https://github.com/qiqihaer/votenet-kitti/blob/master/kitti_demo_files/train_batch/point1.png)

This is the visualization of the votes in one augmentated scene. The groundtruth votes are boxes's centers.
![teaser](https://github.com/qiqihaer/votenet-kitti/blob/master/kitti_demo_files/train_batch/point2.png)

This is the detection results visualization. The red boxes are from prediction results and the yellow ones are from groundtruth boxes.
![teaser](https://github.com/qiqihaer/votenet-kitti/blob/master/kitti_demo_files/results/pred_and_gt.png)
