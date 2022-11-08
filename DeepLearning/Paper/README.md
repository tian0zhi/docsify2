

---
# **论文**
---

<!--
模板：

---
---
### Towards a General Purpose CNN for Long Range Dependencies in ND
**简要概述(采用什么样的方法解决了什么样等问题)：** 利用一种连续卷积神经网络解决数据分辨率、维度和长度在不同场景不同——如，信号采样率不同。   \
**摘要：**  卷积神经网络(CNNs)的使用在深度学习中是广泛的，由于一系列理想的模型属性，这导致了一个高效和有效的机器学习框架。然而，性能CNN架构必须针对特定的任务进行定制，必须考虑诸如输入长度、分辨率和维度等因素。在这项工作中，我们通过我们的连续卷积神经网络(CCNN)克服了CNN架构的缺陷，CCNN是一个配有连续卷积核的单一CNN架构，可以用于对任意分辨率、维度和长度的数据的任务，而不需要结构变化。连续卷积核对每一层的长距离依赖进行建模，消除了当前CNN架构中需要的降采样层和任务依赖深度。通过将相同的CCNN应用于一系列序列(1D)和可视化数据(2D)上的任务，我们展示了我们方法的普遍性。我们的CCNN在所有考虑的任务上都表现得很有竞争力，并且经常超过目前最先进的技术。\
**Abstract:**  The use of Convolutional Neural Networks (CNNs) is widespread in Deep Learning due to a range of desirable
model properties which result in an efficient and effective machine learning framework. However, performant CNN
architectures must be tailored to specific tasks in order to incorporate considerations such as the input length, resolution, and dimentionality. In this work, we overcome the need for problem-specific CNN architectures with our
Continuous Convolutional Neural Network (CCNN): a single CNN architecture equipped with continuous convolutional kernels that can be used for tasks on data of arbitrary resolution, dimensionality and length without structural
changes. Continuous convolutional kernels model long range dependencies at every layer, and remove the need
for downsampling layers and task-dependent depths needed in current CNN architectures. We show the generality
of our approach by applying the same CCNN to a wide set of tasks on sequential (1D) and visual data (2D).
Our CCNN performs competitively and often outperforms the current state-of-the-art across all tasks considered.\
[文章源](https://arxiv.org/pdf/2206.03398.pdf) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[本地源](http://115.159.24.45:3000/DeepLearning/Paper/PDF/2206.03398.pdf)
---


-->

## **卷积神经网络**

---
### Towards a General Purpose CNN for Long Range Dependencies in ND
**简要概述(采用什么样的方法解决了什么样等问题)：** 利用一种连续卷积神经网络解决数据分辨率、维度和长度在不同场景不同——如，信号采样率不同。   \
**摘要：**  卷积神经网络(CNNs)的使用在深度学习中是广泛的，由于一系列理想的模型属性，这导致了一个高效和有效的机器学习框架。然而，性能CNN架构必须针对特定的任务进行定制，必须考虑诸如输入长度、分辨率和维度等因素。在这项工作中，我们通过我们的连续卷积神经网络(CCNN)克服了CNN架构的缺陷，CCNN是一个配有连续卷积核的单一CNN架构，可以用于对任意分辨率、维度和长度的数据的任务，而不需要结构变化。连续卷积核对每一层的长距离依赖进行建模，消除了当前CNN架构中需要的降采样层和任务依赖深度。通过将相同的CCNN应用于一系列序列(1D)和可视化数据(2D)上的任务，我们展示了我们方法的普遍性。我们的CCNN在所有考虑的任务上都表现得很有竞争力，并且经常超过目前最先进的技术。\
**Abstract:**  The use of Convolutional Neural Networks (CNNs) is widespread in Deep Learning due to a range of desirable
model properties which result in an efficient and effective machine learning framework. However, performant CNN
architectures must be tailored to specific tasks in order to incorporate considerations such as the input length, resolution, and dimentionality. In this work, we overcome the need for problem-specific CNN architectures with our
Continuous Convolutional Neural Network (CCNN): a single CNN architecture equipped with continuous convolutional kernels that can be used for tasks on data of arbitrary resolution, dimensionality and length without structural
changes. Continuous convolutional kernels model long range dependencies at every layer, and remove the need
for downsampling layers and task-dependent depths needed in current CNN architectures. We show the generality
of our approach by applying the same CCNN to a wide set of tasks on sequential (1D) and visual data (2D).
Our CCNN performs competitively and often outperforms the current state-of-the-art across all tasks considered.\
[文章源](https://arxiv.org/pdf/2206.03398.pdf) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[本地源](http://115.159.24.45:3000/DeepLearning/Paper/PDF/2206.03398.pdf)
---



---
### Dynamic Routing Between Capsules
**简要概述(采用什么样的方法解决了什么样等问题)：** 设计了一种胶囊神经网络解决传统卷积神经网络只检测特征是否存在而不关心特征位置出现的合理性。   \
**摘要：**  胶囊是一组神经元，其活动向量表示特定类型实体(如对象或对象部件)的实例化参数。我们使用活动向量的长度来表示实体存在的概率，并使用它的方向来表示实例化参数。一个级别的活动胶囊通过转换矩阵对更高级别的胶囊的实例化参数进行预测。当多个预测一致时，一个更高级别的胶囊就会被激活。我们展示了一个经过辨别训练的多层胶囊系统在MNIST上达到了最先进的性能，在识别高度重叠的数字方面比卷积网络要好得多。为了达到这些结果，我们使用了一种迭代路由协议机制：低级胶囊倾向于将其输出发送到活动向量与低级胶囊的预测有一个大标量积的高级胶囊。\
**Abstract:**  A capsule is a group of neurons whose activity vector represents the instantiation parameters of a specific type of entity such as an object or an object part. We use the length of the activity vector to represent the probability that the entity exists and its orientation to represent the instantiation parameters. Active capsules at one level make predictions, via transformation matrices, for the instantiation parameters of higher-level capsules. When multiple predictions agree, a higher level capsule becomes active. We show that a discrimininatively trained, multi-layer capsule system achieves state-of-the-art performance on MNIST and is considerably better than a convolutional net at recognizing highly overlapping digits. To achieve these results we use an iterative routing-by-agreement mechanism: A lower-level capsule prefers to send its output to higher level capsules whose activity vectors have a big scalar product with the prediction coming from the lower-level capsule.\
[文章源](https://arxiv.org/pdf/1710.09829.pdf) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[本地源](http://115.159.24.45:3000/DeepLearning/Paper/PDF/1710.09829.pdf)\
值得参考的网上资源：
- [胶囊网络-Capsule Network](https://zhuanlan.zhihu.com/p/90073690)
- [胶囊神经网络详解](http://t.csdn.cn/a6uvQ)
---