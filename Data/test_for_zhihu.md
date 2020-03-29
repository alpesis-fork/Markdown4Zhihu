本文主要列举了AAAI 2020 Tutorial中关于可解释人工智能的论文选集。


# 可解释人工智能

<img src="https://i.pinimg.com/originals/d1/dd/8a/d1dd8ad36ba93efa683425583d3c4261.png" />

图片来源：AAAI 2020 Tutorial: Explainable AI

可解释人工智能旨在将过去黑盒的人工智能转成可解释的决策推断，从算法、产品到决策，皆为可解释的。

<img src="https://i.pinimg.com/originals/3e/45/7b/3e457b250921961e5c66246702a6b23e.png" />

图片来源：AAAI 2020 Tutorial: Explainable AI

现在存在的问题是：对于监督和非监督学习，推理结果为相关而非因果。而且准确度越高的模型（比如
深度神经网络），其推理结果越没法解释。


模型

- 非线性函数
    - 神经网络 (GAN, CNN, RNN)
    - 组合方法 (XGB, 随机森林)
    - 决策树
- 多项式函数
    - 统计模型 (AOG, SVM)
    - 图模型 (Bayesian Belief Net, SLR, CRF, HBN)
- 拟线性函数
    - MLN
    - 马尔可夫模型
    - 线性模型

# 可解释人工智能在各领域的应用

<img src="https://i.pinimg.com/originals/ce/1e/cd/ce1ecdfab576d3815e6dccf68dd57580.png" />

图片来源：AAAI 2020 Tutorial: Explainable AI

从学习到决策，每个应用领域都有其对应的需要解决的问题。

- **学习**: 人工智能、机器学习
- **决策**: 搜索、博弈论、多智体
- **应用**: 推断(KRR, UAI)、计算机视觉、自然语言处理、机器人学（规划、机器人）

学习

| 类别                    | 模型              | 问题      |

|:------------------------|:------------------|:----------|

| 人工智能                | 代理模型 | 如何总结智能系统行为的动机（动机、理由、理解）以及决策的因果关系？ |

| 机器学习                | 相关图、关键特征 | 哪些特征对分类至关重要？ |


决策

| 类别                    | 模型              | 问题      |

|:------------------------|:------------------|:----------|

| 搜索                    | 冲突消解 | 哪些约束可以放宽？ |

| 博弈论                  | Shapely值  | 哪些特征组合最优？ |

| 规划                    | 规划精细化 | 哪些行为对计划有效？|

| 多智体                  | 策略总结 | 哪个多智体做规划和决策？哪个玩家贡献最多？为什么产生这样的机制？ |


应用

| 类别                    | 模型              | 问题      |

|:------------------------|:------------------|:----------|

| 推理： KRR          | Abduction, Diagnosis | 哪个公理负责推断（比如，分类）？ |

| 推理： UAI          | 基于机器学习 | 非确定性作为可解释的替代 |

| 计算机视觉          | 显著性图、非确定性图 | 哪个复杂特征作为分类？ |

| 自然语言处理        | 基于机器学习       | 哪个实体作为分类？ |

| 机器人学            | 基于可叙述的模型           | 哪些决策或多模态的决策引发行为？ |



## 可解释机器学习

### 可解释模型

<img src="https://i.pinimg.com/originals/ea/d9/cd/ead9cdeaa7ed1c30b4e86d2dc1055737.png" />

图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **朴素贝叶斯模型**
    - Igor Kononenko. Machine Learning for medical diagnosis: history, state of the art and perspective, Artificial Intelligence in medicine, 23:89-109, 2001
- **反事实假设**
    - Brent D. Mittelstadt, Chris Russell, Sandra Wachter: Explaining Explanations in AI. FAT 2019: 279-288
    - Rory Mc Grath, Luca Costabello, Chan Le Van, Paul Sweeney, Farbod Kamiab, Zhao Shen, Freddy Lecue: Interpretable Credit Application Predictions With Conterfacual Explanations. CoRR abs/1811.05245 (2018)

### 人工神经网络

<img src="https://i.pinimg.com/originals/17/8e/09/178e09f30d4eb562466e9284c13a2c23.png" />

图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **深度网络属性**
    - Mukund Sundararajan, Ankur Taly, and Qiqi Yan. Axiomatic attribution for deep networks. In ICML, pp. 3319-3328, 2017
    - Avanti Shrikumar, Peyton Greenside, Anshul Kundaje: Learning Important Features Through Propagating Activation Differences. ICML 2017: 3145-3153.
- **自编码/自原型**
    - Chaofan Chen, Oscar Li, Alina Barnett, Jonathan Su, Cynthia Rudin: This looks like that: deep learning for interpretable image recognition: CoRR abs/1806.10574 (2018)
    - Oscar Li, Hao Liu, Chaofan Chen, Cynthia Rudin: Deep Learning for Case-based Reasoning Through Prototypes: A Neural Network That Explains Its Predictions. AAAI 2018: 3530-3527.
- **注意力机制**
    - Edward Choi, Mohammad Taha Bahadori, Jimeng Sun, Joshua Kulas, Andy Schuetz, Walter F. Stewart: RETAIN: An Interpretable Predictive Model for Healthcare using Reverse Time Attention Mechanism. NIPS 2016: 3504-3512.
    - D. Bahdanau, K. Cho, and Y. Bengio. Neural machine translation by jointly learning to align and translate. International Conference on Learning Representations, 2015.
- **代理模型**
    - Mark Craven, Jude W. Shavlik: Extracting Tree-Structured Representations of Trained Networks. NIPS 1995: 24-30.

### 计算机视觉

<img src="https://i.pinimg.com/originals/40/a5/55/40a5559a091069da07c4a759d6f235a5.png" />

图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **可解释单元**
    - David Bau, Bolei Zhou, Aditya Khosia, Aude Oliva, Antonio Torralba: Network Dissection: Quantifyingn Interpretability of Deep Visual Representations. CVPR 2017: 3319-3327.
- **非确定性图**
    - Alex Kendall, Yarin Gal: What Uncertainties Do We Need in Bayesian Deep Learning for Computer Vision? NIPS 2017: 5580-5590.
- **直观解释**
    - Lisa Anne Hendricks, Zeynep Akata, Marcus Rohrbach, Jeff Donahue, Bernt Schiele, Trevor Darrell: Generating Visual Explanations. ECCV (4) 2016: 3-19.
- **显著性图**
    - Julius Adebayo, Justin Gilmer, Michael Muelly, Ian J. Goodfellow, Moritz Hardt, Been Kim: Sanity Checks for Saliency Maps. NeurIPS 2018: 9525-9536.

## 可解释人工智能

### 博弈论

<img src="https://i.pinimg.com/originals/bd/98/c3/bd98c381e56dd6c873482e8eb436917c.png" />
图片来源： AAAI 2020 Tutorial: Explainable AI

论文参考：

- **Shapley Additive Explanation**
    - Scott M. Lundberg, Su-In Lee: A Unified Approach to Interpreting Model Predictions. NIPS 2017: 4768-4777
- **L-Shapley and C-Shapley (with graph structure)**
    - Jianbo Chen, Le Song, Martin J. Wainwright, Michael I. Jordan: L-Shaley and C-Shapley: Efficient Model Interpretation for Structured Data. ICLR 2019
- **Instance-wise Feature Importance (Causal Influence)**
    - Erik Strumbelj and Igor Konoenko. An efficient explantion of individual classifications using game theory. Journal of Machine Learning Research, 11:1-18, 2010.
    - Anupam Datta, Shayak Sen, and Yair Zick. Algorithmic transparency via quantitative input influence: Theory and experiments with learning systems. In Security and Privacy (SP), 2016 IEEE Synposium on, pp. 598-617. IEEE, 2016.


### 搜索与决策满足

<img src="https://i.pinimg.com/originals/16/77/80/1677801b293f9d4d88a42d93262a9473.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **冲突消解**
    - Barry O'Sullivan, Alexandre Papadopoulos, Boi Faltings, Peral Pu: Representative Explanations for Over-Constrained Problems. AAAI 2007: 323-328
- **稳健性计算**
    - Hebrard, E., Hnich, B., & Walsh, T. (2004, July). Robust solutions for constraint satisfaction and optiimization. In ECAI (Vol. 16, p. 186).
- **约束放松**
    - Ulrich Junker: QUICKXPLAIN: Preferred Explanations and Relaxations for Over-Constrained Problems. AAAI 2004: 167-172.

### 知识表征和推理

<img src="https://i.pinimg.com/originals/d3/95/9f/d3959f5fb9d85619a70fa4a377f21edb.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **解释推理（通过正当理解），如包容**
    - Deborah L. McGuinness, Alexander Borgida: Explaining Subsumption in Description Logics. IJCAI (1) 1995: 816-821
- **诱因推理（贝叶斯网络）**
    - David Poole: Probabilistic Horn Abduction and Bayesian Networks. Artif. Intell. 64(1): 81-129 (1993)
- **诊断推理**
    - Alban Grastien, Patrick Haslum, Sylvie Thiebaux: Conflix-Based Diagnosis of Discrete Event Systems: Theory and Practice. KR 2012

### 多智体系统

<img src="https://i.pinimg.com/originals/62/f3/95/62f3954202c442bfd8be3cc113aa5ac3.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **智能体冲突和有害交互的解释**
    - Katia P. Syncara, Massimo Paolucci, Martin Van Velsen, Joseph A. Giampap: The RETSINA MAS Infrastructure. Autonomous Agents and Multi-Agent Systems 7(1-2): 29-48 (2003)
- **智能体策略归纳**
    - Dfra Amir, Finale Doshi-Velez, David Sarne: Agent Strategy Summarization. AAMAS 2018: 1203-1207
- **可解释智能体**
    - Joost Broekens, Maaike Harbers, Koen V. Hindriiks, Karel van den Bosch, Catholijn M. Jonker, John-Jules Ch. Meyer: Do You Get It? User-Evaluated Explainable BDI Agents. MATES 2010: 28-39
    - W. Lewis Johnson: Agents that Learn to Explain Themselves. AAAI 1994: 1257-1263.

### 自然语言处理

<img src="https://i.pinimg.com/originals/0c/79/4b/0c794b04416b1365ab60c1ca60ec78d8.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **可解释自然语言处理**
    - Hui Liu, Qingyu Yin, William Yang Wang: Towards Explainable NLP: A Generative Explanation Framework for Text Classification. CoRR abs/1811.00196 (2018)
- **自然语言处理LIME**
    - Marco Tulio Ribeiro, Sameer Singh, Carlos Guestrin: "Why Should I Trust You?": Explaining the Predictions of Any Classifier. KDD 2016: 1135-1144
- **自然语言处理调试器**
    - Hendrik Strobelt, Sebastian Gehrmann, Hanspeter Pfister, Alexander M. Rush: LSTMVis: A Tool for Visual Analysis of Hidden State Dynamics in Recurrent Neural Networks. IEEE Trans. Vis. Comput. Graph. 24(1): 667-676(2018)
    - Hendrik Strobelt, Sebastian Gehrmann, Michael Behrisch, Adam Perer, Hanspeter Pfister, Alexander M. Rush: Seq2seq-Vis: A Visual Debugging Tool for Sequence-toSequence Models. IEEE Trans. Vis. Comput. Graph. 25(1): 353-363 (2019)

### 规划与调度

<img src="https://i.pinimg.com/originals/fa/2d/15/fa2d15bb870c5151669f683d4babd097.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **XAI规划**
    - Rita Borgo, Michael Cashmore, Daniele Magazzeni: Towards Providing Explanations for AI Planner Decisions. CoRR abs/1810.06338 (2018)
- **Human-in-the-loop规划**
    - Maria Fox, Derek Long, Daniele Magazzeni: Explainable Planning. CoRR abs/1709.10256 (2017)
- (人工) **规划对比**

### 机器人学

<img src="https://i.pinimg.com/originals/49/62/17/496217a006637b958607990ef63932d8.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **自主机器人体验述说**
    - Stephanie Rosenthal, Sai P Selvaraj, and Manuela Veloso. Verbalization: Narration of autonomous robot experience. In IJCAI, pages 862-868. AAAI Pres, 2016.
    - Daniel J Brooks et al. 2010. Towards State Summarization for Autonomous Robots. In AAAI Fall Symoposium: Dialog with Robots, Vol. 61.62.
- **从决策树到人性化信息**
    - Raymond Ka-Man Sheh: "Why Did You Do That?" Explainable Intelligent Robots. AAAI Workshops 2017

### 非确定性推理

<img src="https://i.pinimg.com/originals/3a/fe/a1/3afea1ad4b55661e8fe50803876c0c9a.png" />
图片来源：AAAI 2020 Tutorial: Explainable AI

论文参考：

- **概率图模型**
    - Daphne Koller, Nir Friedman: Probabilistic Graphical Models - Principles and Techniques. MIT PRess 2009, ISBN 978-0-262-01319-2, pp. I-XXXV, 1-1231

# 参考目录

- AAAI. (2020). [Explainable AI: Foundations, Industrial Applications, Practical Challenges, and Lessons Learned](https://xaitutorial2020.github.io/#)
- Freddy Lecue, Krishna Gade, Sahin Cem Geyik, Krishnaram Kenthapadi, Varun Mithal, Ankur Taly, Riccardo Guidotti, Pasquale Minervini. (2020). [Explainable AI: PPT](https://xaitutorial2020.github.io/raw/master/slides/aaai_2020_xai_tutorial.pdf)

<img src="https://i.pinimg.com/originals/0b/26/e0/0b26e066f574b9be379f427efdf4474c.png" />

