# [Searching for Activation Functions](https://arxiv.org/abs/1710.05941)

_April 2020_

tl;dr: Google (Quoc et al.) used meta-learning to search for better activation functions. Came up with Swish (f(x) = x sigmoid (\beta x)), a non-monotonic, smooth, continuously integratable function that consistently outperforms ReLU (e.g. ImageNet: 0.6% top-1 performance with Inception-ResNet-v2).

#### Overall impression
Well researched and justified piece of work that highlights the efficacy of meta-learning and shows a small but significant improvement of Swish over ReLU across a broad range of metrics and model architectures. Doesn't provide rigorous justifcation for *why* but does attempt to provide a rationale for this improvement and where research efforts should be focussed.

#### Key ideas
- Focused on **scalar activation functions** (scalar in scalar out), which can be used as drop in replacements for ReLU.
- Only searched **unary or binary functions** to limit search space
- The authors found that complicated function performed worse (likely due to optimisation issues) and that periodic functions performed well.
- Swish is defined as f(x) = x sigmoid (\beta x), with \beta being an optional trainable parameter, with it approaching ReLU at x -> inifinity
- Swish is unabounded above and bound below (like ReLU) and **smooth and non-monotonic**, which appear to be key differentiating features.
    - Unbounded above: prevents output saturation (as per e.g. tanh), which prevents efficient learning
    - Bounded below: provides strong regularisation as large negative inputs are dicarded, particularly important at start of learning
    - Smooth: the activation output landscape directly correlates with error landscape. ReLU is not smooth (due to discontinuity). **Easier to optmise smooth error landscape**.
    - Non monotonic (and the non monotonic bump): not really rationalised but a large percentage of pre-activations fall in this regime, suggesting that it is important (increases expressivity of input?)



#### Technical details
- Reinforcement learning-based search using RNN controller trained with Policy Proximal Opt.
- Inital meta-learning training used ResNet-20 on CIFAR-10
- Intermediate testing of top performing functions on CIFAR-100
- Final testing of Swish on ImageNet and WMT 2014 (translation)


