### deepLearningBook
#### deep learning 学习笔记
> - 学习资料来自： 
    - 英文的：http://www.deeplearningbook.org/
        - [完整版pdf下载](https://raw.githubusercontent.com/JDwangmo/deepLearningBook/master/book/deeplearning（带参考文献).pdf)
    - 中文的：http://mp.weixin.qq.com/s?__biz=MzIxMjAzNDY5Mg==&mid=503307054&idx=1&sn=d20623df35d1771dc548d545ed38f318&scene=18#wechat_redirect 


天使(42032089)  19:11:31
中文的是哈工大翻译的Michael Nielsen的《Neural Network and Deep Leraning》
每个小节下面都可以链接到原文

##### 目录：
> - [Table of Contents](https://raw.githubusercontent.com/JDwangmo/deepLearningBook/master/book/www.deeplearningbook.org_contents_TOC.pdf):更详细的目录列表
> - Acknowledgements
> - [Notation](https://raw.githubusercontent.com/JDwangmo/deepLearningBook/master/book/www.deeplearningbook.org_contents_intro.pdf): 使用到的符号说明
> - 1 [Introduction](https://github.com/JDwangmo/deepLearningBook#1-introduction-from-httpwwwdeeplearningbookorgcontentsintrohtml)：
> - [Part I: Applied Math and Machine Learning Basics](https://github.com/JDwangmo/deepLearningBook#part-i-applied-math-and-machine-learning-basics-from-httpwwwdeeplearningbookorgcontentspart_basicshtml)
    - [2 Linear Algebra](https://github.com/JDwangmo/deepLearningBook#2-linear-algebra-from-httpwwwdeeplearningbookorgcontentslinear_algebrahtml)
    - 3 Probability and Information Theory
    - 4 Numerical Computation
    - 5 Machine Learning Basics
> - Part II: Modern Practical Deep Networks
    - 6 Deep Feedforward Networks
    - 7 Regularization for Deep Learning
    - 8 Optimization for Training Deep Models
    - 9 Convolutional Networks
    - 10 Sequence Modeling: Recurrent and Recursive Nets
    - 11 Practical Methodology
    - 12 Applications
> - Part III: Deep Learning Research
    - 13 Linear Factor Models
    - 14 Autoencoders
    - 15 Representation Learning
    - 16 Structured Probabilistic Models for Deep Learning
    - 17 Monte Carlo Methods
    - 18 Confronting the Partition Function
    - 19 Approximate Inference
    - 20 Deep Generative Models

--
##### [1 Introduction](https://raw.githubusercontent.com/JDwangmo/deepLearningBook/master/book/www.deeplearningbook.org_contents_intro.pdf): from http://www.deeplearningbook.org/contents/intro.html
- 我们一直在梦想着创造一个可以思考的机器。
- 人工智能真正的挑战是如何去解决那些人可以很直观解决，但是很难正式描述的事情（如果人类可以很容易正式描述出来的话，就不是难点了，直接一系列规则即可），比如口语理解、人脸识别等。The true challenge to artificial intelligence proved to be solving the tasks that are **easy for people to perform but hard for people to describe formally**—problems that we solve intuitively, that feel automatic, like recognizing spoken words or faces in images. 
- `P1-bottom`：本书就是关于这些直观问题的解决方案，即允许机器从经验中学习，并以一系列**层次性的概念**来理解这个世界（learn from experience and understand the world in terms of a **hierarchy of concepts**），每个概念都是基于更简单的概念或其关系来定义的（with each concept defined in terms of its relation to simpler concepts）。而这层次性的概念也使得计算机可以不断的从 world 中收集知识（人也是这样子学习的），并从更简单的（概念）层次，进而学习更复杂（complicated）的概念.(The hierarchy of concepts allows the computer to learn complicated concepts by building them out of simpler ones.)。如果我们要画一个图来描述这个过程的话，那么可想这个图的深度是非常 deep 的，所以我们把这种方法（solution，解决方案）称作 **deep learning，即层次性学习**。
- 计算机擅长规则或者正式的事情，而不擅长学习不正式或主观的事情： 我们人类每天获取的知识绝多数是来自于人客观或主观的感知，而这是很难以一个正式的方式表达的（Much of this knowledge is subjective and intuitive, and therefore difficult to articulate in a formal way.）。所以计算机若想实现人工智能，一个关键挑战就在于如何将这些非正式的信息传递给计算机（One of the key challenges in artificial intelligence is how to get this informal knowledge into a computer）。有两种方式：
    - 1. hard-code，或者叫做 knowledge base： 即 使用正式语言来对world进行描述（hard-code knowledge about the world in formal languages）,这需要人类设计足够复杂的规则去准确的描述world。但这个太难了，以这种方式构建的系统基本上没有获得巨大成功的。`P2-left`举了个FredWhileShaving的例子，即Cyc系统（knwoledge base system）无法理解 在早上剃胡须的Fred（人名）这是个什么东西，因为它认为人不是不应该包含电子器件的，但是FredWhileShaving又包含了电子器件，所以它会检测到不一致性。
    - 2. **machine learning（ML）： hard-code面临的困难也意味着，机器应该拥有取获取自己知识的能力，即从原始数据（底层）到规则/模式（高层）的获取知识的能力，这个能力就叫做机器学习（ML）**。简单的机器学习算法比如有：逻辑回归模型（LR）、朴素bayes（NB）。
        - **这些简单机器模型的基本流程是输入数据的某种表示形式（data reprezation，or feature ，特征，经常需要人工提取），接着去学习这些输入和输出的关系。**也就是这些简单机器学习算法严重依赖数据的表示形式，特征造得好和坏，对结果影响特别大（It is not surprising that the choice of representation has an enormous effect on the performance of machine learning algorithms）。
        - 对于简单的任务，我们可以很容易的提取出有价值的特征，然后丢给一个简单机器学习算法去学习即可完美解决该任务的问题。但是**对于很多任务，是很难去知道要提取哪些特征的**。比如，假设我们想取写一个程序取检测图像中的cars，因为我们直到cars有轮子（wheels），那么我们就可以以是否有轮子来作为特征。但是非常unfortunately，机器并不知道轮子是怎样子（ it is difficult to describe exactly what a wheel looks like in terms of pixel values），甚至轮子还可能出现光照、阴暗等的影响等等。
        - **representation learning: `P4-top`. 那么数据表示的问题（特征）这个问题的一个解决方法就是机器学习不仅去发现从数据表示（特征）到输出之间的关系，同时也去学习数据表示形式自身（原始输入到特征的mapping）**,这就叫做**表示学习或特征学习**。同时学习到的数据表示（特征）也比人造的特征表现要好。
            - 特征学习和映射学习两者同时学的好处在于实现了end-to-end的学习，这使得AI系统可以快速的迁移到一个新任务，而不需要人工造任何的特征（减少人工干预，更智能）。一个好的representation learning算法甚至可以在几分钟学习到一个简单任务的良好特征集合。大大减少了人造特征的工作量。
            - algorithm example: 
                - autoencoder（自编码）：`P4-bottom`.由一个encoder函数和一个decoder函数构成。An autoencoder is the combination of an encoder function that converts the input data into a different representation, and a decoder function that converts the new representation back into the original format.可以用encoder的输出作为数据的表示形式。

#### [Part I: Applied Math and Machine Learning Basics](https://raw.githubusercontent.com/JDwangmo/deepLearningBook/master/book/www.deeplearningbook.org_contents_part_basics.pdf): from http://www.deeplearningbook.org/contents/part_basics.html

##### [2 Linear Algebra](https://raw.githubusercontent.com/JDwangmo/deepLearningBook/master/book/www.deeplearningbook.org_contents_linear_algebra.pdf): from http://www.deeplearningbook.org/contents/linear_algebra.html

#### [3 Probability and Information Theory]
