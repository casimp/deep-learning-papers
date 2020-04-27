# [YOLOv4: Optimal Speed and Accuracy of Object Detection](https://arxiv.org/abs/2004.10934)

_April 2020_

tl;dr: Improving AP at high inference FPS (trainable on signle GPU) by combining universally applicable architecture features (e.g. backbone agnostic). 

#### Overall impression
This is a reasonably well written paper, which provides a concise background to object detection architecture features (perhaps overly concise wrt. some features). State-of-the-art performance is achieved through a refined/combined selection of these features. The authors refer to 'new features' being implement (e.g. mosaic data augmentation) these are relatively new within literature, not new in this paper. 

Emphasis is on inference FPS, so the authors implement features that are free (bag of freebies) or have minimal impact (bag of specials) at inference time. The authors then modify features to ensure that single GPU training is feasible.


#### Key ideas
- YOLOv4 splits object detectors into 3 parts: Backbone (e.g. ResNet), Neck (e.g. feature extractor)  and Head (e.g. classifier). Evaluates most efficient/accurate features to implement at each stage. They split features into: 
	- 1) Bag of freebies (BOF) --> **improves accuracy without affecting inference FPS (e.g. data augmentation)**
	- 2) Bag of specials (BOS) --> **improves accuracy with limited impact of inference FPS (e.g. Spatial Attention Module - improves 0.5% top1 accuracy, only 0.1% inference increase)**
- Systematically assess the impact of a very wide range of the existing BOF/BOS on classifier and detector training
- The authors suggest the features they implement can be used as best-practice in future studies


#### Technical details
- Some new features that were successful:
    - **Mosaic data augmentation** (mosaic of 4 images)
    - Using different loss function for bounding box regression, most notably **Generalised IoU** (considers shape/orientation of BBox), **Complete IoU** (considers distance between centre points)) 
    - Mish activation - improvement over Swish (and Leaky-ReLU, which is default)
    - Genetic algorithms for hyper-param selections (during first 10% of training)
- CSPDarknet-53 and CSPResNeXt-50 used as backbones(CSP - Cross-Stage-Partial Connections)
- SOTA real-time inference FPS for consumer graded GPUs (8 - 16GB VRAM)
- Comparable performance to EfficientDet (D0-D2) at much higher FPS

#### Notes
- [GitHub page](https://github.com/AlexeyAB/darknet) 

