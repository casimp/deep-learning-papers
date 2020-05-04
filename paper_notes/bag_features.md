# [Approximating CNNs with Bag-of-local-Features models works surprisingly well on ImageNet](https://arxiv.org/abs/1904.00760)

_April 2020_

tl;dr: Scramble an image in mid sized chucks and a CNN will give you a similar result - deep neural networks are largely reliant on local features. Bag of features (BoF) type (chunked) models shed light on this and are much more interpretable without large loss in accuracy.

#### Overall impression
Fantastic paper. Well researched and novel, provides genuine insights into the workings of all CNNs and offers up the BoF method for improved CNN interpretability. Shows that CNNs are not doing anything significantly different to 'traditional' methods, but are just doing this very well.

#### Key ideas
- Prior to CNNs, top image recognition prizes were won by algorithms which used BoF approaches (finding discriminative local visual features and 'counting' these without consideration of global context)
- Authors use the same approach to a CNN - very small receptive field (9, 17, 33) used to classify local regions and then combine the class counts
- Provides a heat map of the discriminative features for each class
- You can then look at mis-classified images and understand what features were causing this through this heat map
- For BoF, as you remove sections of the image the accuracy reduces linearly as a function of the number of positively activated features
- With shallower networks (VGG-16) you see a very similar response to BoF wrt. image chunk removal. Deeper, more complex models still exhibit this response but less strongly. They are learning information that is more semantic (global, contextual)


#### Technical details
- BoF has a similar structure to ResNet, but switching 3x3 convolutions to 1x1 to limit receptive field
- Outputs from final local receptive field are converted into logits and linearly combined - this linear combination is key to interpretability.

### Notes

The author W. Brendel says in a tweet: 

> “…we need to be careful: the availability of many weak and local statistical regularities can be sufficient to solve the task in which case DNNs do not learn the underlying “physics” of the world (like object shape). We need better tasks.”

