---
published: true
title: 如何从Rosalind Franklin的衍射实验中观察出DNA双螺旋结构？
layout: post
author: Yu
category: 论文笔记
tags:
- Rosalind Franklin
- X-ray衍射
- DNA双螺旋结构
---

> 本文是一篇物理实验论文的介绍和编译，由于我对文中可能涉及的概念理解有误，希望看到的读者能够指出。
>
> **本篇文章未经授权，请勿转载。**


罗莎琳德·埃尔西·富兰克林(Rosalind Elsie Franklin)是一名实验物理学家（1920-1958），她使用X射线衍射方法探测到了DNA的结构。

“从那张经典的DNA晶体衍射图片(<q>Photo 51</q>)里能读到什么信息来证明DNA的结构？” 一直是我非常感兴趣的问题。之前问过学生物的同学，他们也不清楚。由于我看不懂X射线衍射图像，在网上找了一些解读的文章，发现了[这篇论文](http://homepages.ius.edu/kforinas/P105/PTE000140.pdf "How Rosalind Franklin Discovered the Helical Structure of DNA: Experiments in Diffraction")，用简单的中学实验方法讲述了富兰克林（以下用姓氏代替全名）的发现。
<q>2017年续，其实看了上面那篇文章，我还是没有弄懂究竟为什么图像是这个样子，经过一番搜索，我找找到了[Diffraction by DNA, carbon nanotubes and other helical nanostructures](http://iopscience.iop.org/article/10.1088/0034-4885/68/5/R05)这篇文章，螺旋结构的衍射图像就是富兰克林Photo 51中的样子。一直没理解的问题，其实是由于自己物理没学好，无法理解衍射图像。再后来看到quora上的问题[How does one physically interpret the different diffraction patterns between A-DNA and B-DNA?](https://www.quora.com/How-does-one-physically-interpret-the-different-diffraction-patterns-between-A-DNA-and-B-DNA)，从答案中可以看到原始模型，光学仿真以及衍射图像排列在一起的样子。</q>

![A-DNA_and_B-DNA](http://i.imgur.com/Cb2TpAz.png)


在1951年11月的一份讲义中，富兰克林写到：这个结果支持DNA是一个螺旋结构，每个螺旋单元里包含（必须非常紧密排列的）2，3或者4个共轴核酸链，并且外侧有磷酸基团（The results suggest a helical structure (which must be very closely packed) containing 2, 3 or 4 co-axial nucleic acid chains per helical unit, and having the phosphate groups near the outside.）。这个结论比沃森（J. D. Watson）和克里克（F. Crick）公布他们基于富兰克林衍射图片对于DNA结构进行的研究要早了将近16个月。沃森和克里克是如何得到衍射图片数据的？这个在本文中不会涉及，沃森和克里克最终获得了诺奖，他们和富兰克林之间的往来是另一个吸引人的关于性格不和和男性沙文主义的故事，想了解整个发现过程，请搜索`DNA - Secret of Photo 51(Nova)`这部科学纪录片。

在<q>How Rosalind Franklin Discovered the Helical Structure of DNA: Experiments in Diffraction</q>这篇论文中，作者设计了四个实验，使得学生可以重走富兰克林的DNA结构发现之旅，并且这些实验条件简单可以在高中或者大学本科实验室中重复。在实验中，作者用圆珠笔的弹簧来代替DNA，用普通光线来代替X射线。这些实验是一个普通的单缝或多缝衍射实验的相对简单扩展。它们可以向学生展示在一般实验室中无法很好说明的“衍射技术实用性”问题。
四个实验中的设备条件和困难程度各不相同。实验1使用简单的设备来说明衍射如何揭示了一个对象的结构。实验2需要一个稍微复杂的设置，同时也提供了有关衍射对象的详细信息。实验3是<q>Photo 51</q>的分析，实验4是一个螺旋线的衍射的计算机模拟。实验1,2和3都是不错的课堂演示。

![Photo_51](http://i.imgur.com/vzJogUJ.png)

图片为罗莎琳德·富兰克林X射线衍射实验获得的B型DNA衍射图案（图片编号：Photo 51）。图中最大的圆圈的直径为94mm。在零级衍射斑的位置有铅盘覆盖，以免曝光过度。一级衍射斑的位置也基本被覆盖住了，所以在实验中我们只使用二级，三级和五级衍射斑进行计算，四级衍射斑缺失，在文中会有说明。

### 为什么X形图案揭示了双螺旋的结构？

下面我们用一个简单的实验来介绍单缝衍射。如果我们用投影仪照射一个圆珠笔里的弹簧，可以得到下图中的图像，那么如果我们用一只激光笔或者激光二极管与投影仪一样从同样的方向来照射同样的弹簧，可以看到与投影仪照射时类似的结果(<q>类似个屁，我就是没弄清楚这个地方[^1]</q>)。由于光源的直径有限，所以只能照射到弹簧的一部分区域（例如没有照射到一部分弹簧线拐弯处时，线圈如同八字形或者倒八字形，两条“腿”的样子）。我们还可以用一个透镜来放大这个图形，投影到墙上。

![projection_pattern_of_spring](http://i.imgur.com/hVNBbmw.png)

根据巴比涅原理（Babinet’s principle states），在点光源照射下，一个不透光物体产生的衍射图样和一个带有与该物体形状、大小完全相同的孔的衍射屏产生的衍射图样完全相同。 那么线圈被照射的部位的图形，也就与同样形状的单缝衍射图形一样。

如何求出DNA的半径呢？通过一个缝隙的衍射无法得到半径，我们只能通过衍射暗斑来计算遮挡物体的宽度（弹簧铁丝的厚度 $$\alpha$$），在角度为$$\theta_{min}$$的时候$$\alpha$$的可以通过$$\alpha sin \theta_{min} = m \lambda$$求得。但是DNA没有“厚度”这个概念，因为x射线衍射测得是重磷核（heavy phosphorous nuclei）。

### 富兰克林如何测得DNA的直径

我们可以通过增加两个凸透镜来扩大激光照射的范围，如下图所示。

![far-field_diffraction_pattern_design](http://i.imgur.com/Gm26M5E.png)


通过衍射实验，我们可以得到弹簧线圈的多个间距，为了得到半径，需要首先知道间距的数值P。间距是螺旋之间的距离，也就是sin函数的波长。
![sine-function](http://i.imgur.com/vWrkyfr.png)

通过上图我们可以从图中得到间距P可以由两个螺旋圈之间的距离d除以$$cos\alpha$$得到。$$P=\frac{d}{cos\alpha}$$。

那么为什么我们还要测量多个螺旋圈之间的距离来的推断d呢？ 衍射峰在角度为$$\theta_{min}$$的时候的计算公式为：$$d sin\theta_{max} = m \lambda$$。

我们用带有两个凸透镜的装置（上上图），可以求得透镜之间的距离是$$f_1+f_2$$，假设我们将光束的直径扩大到$$w=7$$毫米，并且得到5个sine函数间距（实验中一定要注意不要把平行光源弄成发散的）。当距离$$D>=w^{2}/\lambda$$时（w时光束直径，$$\lambda$$时波长），衍射图像属于远场衍射图（夫琅和费衍射）。实物图像如下图所示。

![far-field_diffraction_pattern](http://i.imgur.com/8f1t65T.png)

为了在更近的距离得到衍射图像，我们需要调整透镜之间的距离。之后就会看到弹簧的衍射图像呈现出亮斑的样子。在衍射暗斑的范围内，一些亮点是模糊的或者会看不到（丢失）。衍射暗斑是由于线圈的厚度所引起的干涉现象造成的。在计算圈数时一定别忘了包含丢失的圈。计算半径时，我们先选取第18个衍射峰，度量其到中心最大到光斑到距离（27mm，用游标卡尺[^2]），然后使用$$d sin\theta_{max} = m \lambda$$。这个公式计算出d，即平行的两个线圈之间的距离是1.77mm，接下来根据$$P=\frac{d}{cos\alpha}$$，就可以求出P（角度应该是测量值）。投影的Sin函数波的斜率就是sin波函数的梯度，当x=0时，$$R sin(\frac{2\pi}{P\cdot x})$$，对左边当x=0时求微分，结果为$$\frac{2\pi R}{P}=tan(90 ^\circ -\alpha)$$。

### 从DNA衍射照片中计算半径

上面同样的方法可以应用于从DNA衍射照片中计算半径，将衍射图像按原始大小打印（直径94mm）。假设富兰克林当时使用的波长是铜$$K_{\alpha}$$线($$\lambda=0.15 nm$$)，样本和投影之间的距离是9cm。接下来就可以确定P，角度以及DNA的半径了。图像中0级和1级衍射峰被屏蔽（因为他们会在胶片上被过度曝光），所照片上离中心最近的光圈是2级（阶），我们可以用2，3，5级（阶）光圈来计算P值。<u>富兰克林将第4级（阶）光圈的缺失归结为是有第二个螺旋，即双螺旋！！！其偏移为螺距的3/8</u>

> The structural unit probably consists of two co-axial molecules which are not equally spaced along the fibre axis,… If one molecule is displaced from the other by about three-eighths of the fibre- axis period, this would account for the absence of the fourth layer line maxima and the weakness of the sixth.

第一个螺旋的第4阶衍射峰出现在第二个螺旋第第2阶衍射暗斑处，双缝衍射的光斑在其中一个单缝的衍射暗斑处消失。

### 计算机模拟衍射图像

根据惠更斯原理，衍射图案由从孔径出现的所有基本波“融合”而成的，球形波面上的每一点（面源）都是一个次级球面波的子波源，子波的波速与频率等于初级波的波速和频率，此后每一时刻的子波波面的包络就是该时刻总的波动的波面。其核心思想是：介质中任一处的波动状态是由各处的波动决定的。
因此我们可以通过从光圈到x和y方向出现的所有正弦波（和余弦波）上求积分的方法来计算衍射图像。弹簧的衍射图像可以用产生正弦波的两个函数叠加而成。

$$Rsin\frac{2\pi x}{P}+\frac{\alpha}{2}$$ 和 $$Rsin\frac{2\pi x}{P}-\frac{\alpha}{2}$$，其中$$x_1<x<x_2$$。衍射图形$$F^2(k_x,k_y)$$ 可以从下图中得到。
![eq5](http://i.imgur.com/FR4LQbs.png)
这个结果是一个关于空间频率的函数，有了$$k_x$$和$$k_y$$ 就可以画图了。

文章后面还有一个具体的例子，公式书写太麻烦，不再赘述。



-Q.E.D.-


后记：关于如何从DNA的X射线衍射图片中推测出DNA的结构的疑问，从我第一次看到那张图片起，就一直环绕在脑中，读研究生期间也没从老师同学那里得到答案，直到2013年我发现了DNA Learning Center里的这个[slide](http://www.dnalc.org/view/15874-Franklin-s-X-ray.html)，隐约从图中建立起了螺旋结构和衍射图片的联系，但是我还是没弄明白（自己的空间想象力和物理学知识都太差）。
2014年年初，我又翻出了这个问题，从果壳搜到一篇[问答](http://www.guokr.com/question/487450/)，我依旧没有看明白，不过那篇问答的作者给出了《物理教师》期刊中的论文，这篇论文<del>最终</del>也没能解答了我的问题。在2017年我翻到旧博客，决定彻底解决这个问题的时候，还参考了[Diffraction by DNA, carbon nanotubes and other helical nanostructures](http://iopscience.iop.org/article/10.1088/0034-4885/68/5/R05) 这篇文章。<u>一直没能理解这个图像的原因是我不知道螺旋结构的衍射图案的样子。</u>

从我产生这个问题到自己最终弄明白经过了很多年的时间，在没有得到任何帮助的情况下，自己都感到太不容易了。

注释：

[^1]: 我用发光二极管和圆珠笔弹簧在封闭无光的厕所内重复了这个实验，由于不是“点”光源，所以衍射效果不好，近距离基本和投影仪的图像一样，远距离比较模糊，但只能看出“1圈衍”射的效果。没图，在暗室里手机没法拍照。

[^2]: DNA无法用游标卡尺测得光斑之间的距离，我们唯一的信息来源是衍射图像。
