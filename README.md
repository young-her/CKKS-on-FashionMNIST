# CKKS-on-FashionMNIST
本项目实现了基于CKKS方案同态加密的深度学习模型,可在密文上进行卷积神经网络训练和预测,为保护隐私数据提供了有效方案。主要工作包括:
1.搭建明文神经网络模型,在FashionMNIST数据集上进行训练和评估,获得88%的准确率。
2.优化神经网络结构,采用折叠线性层技术,将多个线性层合并为一个新层,减少同态加密运算开销。优化后的网络在密文上的预测准确率也达到88%,与明文模型相当。
3.调整CKKS加密参数,平衡运算精度、安全性和效率。包括设置多项式模数度、系数模比特长度和缩放因子等。
4.实现基于CKKS的各种同态运算,包括卷积、池化、非线性激活和全连接等操作。

本项目的缺点：
1.训练模型的开销还是比较大，在GTX4090，12核CPU的服务器上面跑第一种加密模型一轮只需2s左右，而优化后的模型跑一轮90s左右。
2.由于电路深度的限制，神经网络的层数也被限制，如果想进行多次卷积，则会导致多项式系数模度数变得非常大，同态运算开销同时也暴增，实用性大大降低。
3.激活函数的限制，本项目采用最简单的非线性多项式激活函数，即平方激活。其非线性程度可能不足以处理复杂的数据模式。相比之下，像ReLU或tanh这样的激活函数能够提供更强的非线性，使得模型能够学习更复杂的模式。平方激活函数没有像sigmoid或tanh那样的自然边界，无法防止激活值过大或过小，这可能会导致模型的稳定性降低。
## 参考文献
[1]Cheon J H, Kim A, Kim M, et al. Homomorphic encryption for arithmetic of approximate numbers[C]//Advances in Cryptology–ASIACRYPT 2017: 23rd International Conference on the Theory and Applications of Cryptology and Information Security, Hong Kong, China, December 3-7, 2017, Proceedings, Part I 23. Springer International Publishing, 2017: 409-437
[2]张慈.基于同态加密的隐私数据卷积神经网络预测[J].[2024-06-15].
[3]Chou E , Beal J , Levy D ,et al.Faster CryptoNets: Leveraging Sparsity for Real-World Encrypted Inference[J].  2018.DOI:10.48550/arXiv.1811.09953.
