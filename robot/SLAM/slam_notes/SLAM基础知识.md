##SLAM基础知识SLAM基础知识
[TOC]
###SLAM介绍
SLAM(Simultaneous Localization and Mapping).**即时定位与地图构建**
- 更多详细的介绍，参看高翔博士维护的slam网站  [SlamCN](http://www.slamcn.org/index.php)。这一网站上，呈现了主流的开源SLAM方案以及提供了入门资料、国外高校SLAM教学视频。此外，高翔博士的博客园博客账号上，分享了大量的SLAM的学习心得和手把手搭建教程。值得学习，[博客地址
](http://www.cnblogs.com/gaoxiang12/)

###SLAM开发语言和平台
- C/C++
- Python
- Matlab
- Ubuntu(Linux 推荐使用Ubuntu)

###SLAM学习资料汇总
1. **主要的SLAM资料汇总来源**
[SLAM学习资料整理](http://www.cnblogs.com/wenhust/p/5942893.html)
[高翔博士博客](http://www.cnblogs.com/gaoxiang12/)
2. **额外的学习资料**
在知乎上，有一片高质量的SLAM学习问答，奉上帖子。
[学习SLAM需要哪些预备知识？](https://www.zhihu.com/question/35186064)
特别喜欢，这篇帖子中 **王小新** 的回答。引用如下：
> 作者：王小新
> 链接：https://www.zhihu.com/question/35186064/answer/135059903
> 来源：知乎
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
　　感觉大家的回答都很好，但是作为一个从新手到微新手过来的人，觉得大家回答上来就是 Multiple View Geometry in Computer Vision  然后优化，然后。。。。，如果新手这样做的话光啃那本书就是3个月+。
　　我建议首先了解SLAM主要采用什么做的，历史上一些版本是如何做出来的，因为这个系统是一个比较庞杂的系统，也表明，最开始这个系统的并不是如此，只是随着时间的推移，让这个系统复杂起来。
　　粗略的了解了SLAM系统的概况之后，进一步研究所需要的东西，只有知道所需要的东西，才能知道自己差在什么地方。比如：目前SLAM基本分支有 激光、单目、双目和RGBD 四种，建议根据自身条件主要学习一种就可以。
　　然后就会发现，SLAM获取数据采用滤波的方法，有卡尔慢滤波、EKF、UKF、EIF、PF、RBPF、FASTSAM等，然后就发现自己应该学什么滤波了，为进一步研究，又发现，有的SLAM用图优化，如ORB-SLAM  所以需要了解g2o ，g2o 主要是什么，通过代码发现 里头有非线性最小二乘法：牛顿高斯、LM，自己推到一遍，然后就学吧。然后就发现，在使用单目的时候有很多东西都是获取不到，怎么办呢？这个时候看SLAM代码和论文，发现需要学习PNP，逆深度，三角重建，之后就能通过摄像头画出自己的轨迹和重建了，之后发现自己的轨迹怎么不对呢，精度不够，然后就要BA出马了。这些搞懂了，突然发现SLAM会了一半了，图有了，就该优化了，如何优化？？ 通过论文就会发现，闭环检测！！！是个好方法，通过学习闭环检测，就可以将词袋模型，全局优化方法进行学习，然后发现最致命的问题，尺度统一不了，怎么办！！Sim(3) 算法来了，可以解决一部分尺度问题。最后你的SLAM就差不多了。
　　这些学习完事之后，你会发现，你会了基本的优化方法、滤波方法、图像处理方法、矩阵更加熟悉，知道了什么是李群李代数在计算几何中的使用。
　　最后推荐一篇论文：Local Accuracy and Global Consistency for Efficient Visual SLAM 作者 Hauke Strasdat  帝国理工大学
　　非常的棒书：《Multiple View Geometry in Computer Vision》
　　基础书：《线性代数应该这样学》
　　数据集:Tum   MRP Kitti ICDL-NUIM

给出一个思维导图
![](https://pic3.zhimg.com/v2-57adda9336a521d6fd4bb750e3d2cb82_b.png)

###下一步学习计划
计划用１～２周的时间
1. 学习完入门资料《SLAM for Dummies》，这本书上面有大量的代码帮助理解。
2. 再是跟着　高翔博士　实现第一个SLAM实战　[一起做RGB-D SLAM (1)](http://www.cnblogs.com/gaoxiang12/p/4633316.html)
3. Google的Cartographer开源代码学习