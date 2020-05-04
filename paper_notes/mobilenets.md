# [MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications](https://arxiv.org/abs/1704.04861)

_April 2020_

tl;dr: Using depth-wise seperable convolutions to reduce theoretical computational overhead by a factor of ~10. Basis of a new family of model architectures (inc. EfficientNet).

#### Overall impression
Well written paper, with results tested across a representative array of scenarios. While there is a significant reduction in params and mult-adds, the authors  do not highlight the **actual train time**, which does not always scale well with params.

#### Key ideas
- Standard convolutions can be replaced by depth-wise  seperable convolutions. Effectively factorising the conv into a depthwise conv and a 1x1 operation 
- Theoretical computation then scales with 1/Dk^2 relative to standard convolutions, where Dk is the convolution size. So, for a 3x3 convolution, there is a 9x reduction in resource. 
- Authors also play with the width and resolution to try to find an optimal balance i.e. scale the model down while retaining as much accuracy as possible.

#### Technical details
- For an input feature map of size Df x Df x M a typically conv filter would have a shape Dk x Dk x M x N (where N is the number of channels) and output size Dk x Dk x N. 
- Depthwise separable splits this into a Dk x Dk x M operation (outputting Df x Df x M), which feeds into a 1 x 1 x N operation, which outputs a Df x Df x N feature map.

#### Notes
- Theoretically, the depthwise separable convolutions are very efficient but there may be issues (as with EfficientNet). The below article goes into more detail, but seems like they are not well optimised/implemented compared to stand convolutions.
https://tlkh.dev/depsep-convs-perf-investigations/ 

