---
{"dg-publish":true,"permalink":"/reading-notes/a-unified-approach-to-interpreting-model-predictions/"}
---


# 《A Unified Approach to Interpreting Model Predictions》论文解读
@lundbergUnifiedApproachInterpreting2017

## Introduction
- The growing availability of big data has increased the benefits of using complex models
- Present a novel unified approach to interpreting model predictions
	- the perspective of viewing any explanation of a model’s prediction as a model itself, which we term `the explanation model`.
	- propose SHAP values as a unified measure of feature importance that various methods approximate.
	- propose new SHAP value estimation methods and demonstrate that they are better aligned with human intuition

## Interpretation model properties
描述解释模型需要有的三个性质，而现在解释方法的缺陷[^1]
- 局部准确性：如果x‘是x的简化特征，对应解释模型g(x') = f(x)，即解释模型在给定的特征情况下能解释为什么模型预测值是这么多。
- 缺失性：当x'=0的时候，贡献度$\phi$为0
- 一致性：模型改变导致特征变的更重要时，贡献度也应该变大

![](https://cdn.jsdelivr.net/gh/jmwyf/pichosting@master/tree.png)
上图模型A发热和咳嗽直觉上重要程度应该是一样，模型A和B分别的特征重要度也应该一样。

## **Additive Feature Attribution methods**
一大类方法中解释模型是一系列二元变量的线性函数
称为**Additive Feature Attribution methods**（AFA）相加特征归因方法

## Classic Shapley Value Estimation
$$\phi_{i} = \sum_{S \subseteq F\backslash\{i\}}\frac{|S|!(|F|-|S|-1)!}{|F|!}[f_{S\cup\{i\}}(x_{S\cup\{i\}})-f_{S(x_S)}]$$
基于上面公式计算很麻烦，从F中选取S特征有$2^F$种方式，计算量巨大


## SHAP
SHAP分为模型无关和模型相关两类方法，模型无关的代表是kernelSHAP，而模型相关的代表则有DeepSHAP和TreeSHAP，一个是针对深度学习，一个是针对树模型。

## Kernel SHAP
### LIME
LIME[^2]（Local interpretable model-agnostic explanations)（why should I trust you: Explaining the predictions of any classifier）通过生成的包含需要解释点周围的扰动数据和基于黑箱模型预测结果的数据集，训练一个可以解释的模型，比如逻辑回归、决策树，这个可解释模型需要在解释点周围达到较好的效果。
$$\xi = \mathop{\arg\min}\limits_{g\in G}L(f,g,\pi_x) + \Omega(g)$$
- f为需解释模型
- g为可能的解释模型
- $\pi_x$为定义实例周围多大范围
算法过程：
- 选择需要解释感兴趣的实例
- 对其进行扰动，并得到黑箱模型对应结果产生新数据集
- 根据与实例的接近程度，对新数据集进行赋予权重
- 基于新数据集训练可解释模型
- 解释预测值
![](https://cdn.jsdelivr.net/gh/jmwyf/pichosting@master/weightshap.png)
Figure 3: Toy example to present intuition for LIME

### KernelSHAP（Linear LIME + Shapley value）
LIME（Local interpretable model-agnostic explanations）方法的拓展，通过修改LIME需要求解loss等式参数，其主要思路是利用核变换，让$\phi$符合shapley value[^3]
算法过程[^4]：
- 从M个特征中抽样k，$z_k^{'} \in \{0, 1\}^M$
- 计算黑箱模型预测值
- 基于SHAP kernel计算$z_k^{'}$ 样本权重，$z_k$里面1的个数不一样权重就不一样
- 拟合线性模型
- 从线性模型中返回Shapley values
SHAP核为(推导过程见2补充材料)：$$\pi_{x'}(z')= \frac{(M-1)}{(M choose |z'|)|z'|(M-|z'|)}$$
$$L(f,g, \pi_{x'})=\sum_{z'\in Z}[f(h_x^{-1}(z'))-g(z')]^2\pi_{x'}(z')$$
x'为简化输入，$x=h_x(x')$, $z' \subseteq x'$

## Deep SHAP
### DeepLIFT（Learning Important FeaTures）
DeepLIFT[^5]方法使用神经元的激活与其“参考”进行比较，其中参考是神经元在网络获得“参考输入”时具有的激活状态（参考输入根据适合手头任务的内容定义）。该方法赋予每个特征重要度分数之和等于预测值与基于参考输入的预测值之间的差异[^6]。
能解决基于梯度方法的不足，例如参考的差异不是0的情况下梯度仍然可能是0。
$$\sum_{i=1}^n C_{\Delta x_i \Delta t} = \Delta t \tag1$$
$\Delta t = t - t^0$, 神经元输出与参考输出的差异，$\Delta x$输入相对参考输入的变化， C即神经元的贡献

$$m_{\Delta x\Delta t} = \frac{C_{\Delta x\Delta t}}{\Delta x} \tag2$$
定义乘子multiplier，满足链式法则
算法步骤[^7]：
- 定义参考值
	- choosing a good reference would rely on domain-specific knowledge, and in some cases it may be best to compute DeepLIFT scores against multiple different references
	- 比如图像用全0或者模糊版本，基因数据用本底期望频率
- 区分正负贡献（2019）
- 贡献度规则
	- 线性层直接是系数$w* \Delta x_i$
	- 非线性变化是$m_{\Delta x\Delta y} = \frac{C_{\Delta x\Delta y}}{\Delta x} =\frac{\Delta y}{\Delta x}$

### DeepSHAP(DeepLIFT + Shapley value)
尽管kernelSHAP是适用于所有模型的包括深度学习模型的一种可解释方法，但是有没有能利用神经网络特性的可解释方法从而提高计算效率。
DeepLIFT计算的分数近似于Shapley value?
- the Shapely values measure the average marginal effect of including an input over all possible orderings in which inputs can be included. If we define “including” an input as setting it to its actual value instead of its reference value, DeepLIFT can be thought of as a fast approximation of the Shapely values[^8]
![](https://cdn.jsdelivr.net/gh/jmwyf/pichosting@master/components.png)
![](https://cdn.jsdelivr.net/gh/jmwyf/pichosting@master/shap.png)
figure form [3]
- 基于Shapley value的定义以及公式可以看出重要的一部分即边际效应，即模型包含该特征减去未包含该部分。在上述一个神经网络模块里面，特征顺序选择都不存在。
- 把用实际值代替参考值看作是包含某个特征，DeepLIFT方法



#XAI #SHAP

[^1]: [6 – Interpretability – Machine Learning Blog | ML@CMU | Carnegie Mellon University](https://blog.ml.cmu.edu/2020/08/31/6-interpretability/)
[^2]: Ribeiro, M. T., Singh, S. & Guestrin, C. ‘Why Should I Trust You?’: Explaining the Predictions of Any Classifier. _Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining_ 1135–1144 (2016) doi:[10.1145/2939672.2939778](https://doi.org/10.1145/2939672.2939778).
[^3]: [A Unified Approach to Interpreting Model Predictions](https://papers.nips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html)
[^4]: [9.6 SHAP (SHapley Additive exPlanations) | Interpretable Machine Learning](https://christophm.github.io/interpretable-ml-book/shap.html)
[^5]: [deeplift 0.6.13.0 on PyPI - Libraries.io](https://libraries.io/pypi/deeplift)
[^6]: [Explainable Neural Networks: Recent Advancements, Part 3 | by G Roshan Lal | Towards Data Science](https://towardsdatascience.com/explainable-neural-networks-recent-advancements-part-3-6a838d15f2fb)
[^7]: Shrikumar, A., Greenside, P., Shcherbina, A. & Kundaje, A. Not Just a Black Box: Learning Important Features Through Propagating Activation Differences. Preprint at [https://doi.org/10.48550/arXiv.1605.01713](https://doi.org/10.48550/arXiv.1605.01713) (2017).
[^8]: Shrikumar, A., Greenside, P. & Kundaje, A. Learning Important Features Through Propagating Activation Differences. Preprint at [http://arxiv.org/abs/1704.02685](http://arxiv.org/abs/1704.02685) (2019).
