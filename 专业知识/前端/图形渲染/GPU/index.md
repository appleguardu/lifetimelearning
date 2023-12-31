# GPU
https://cloud.tencent.com/developer/article/1814898
WebGL 的核心是 OpenGL，它是 OpenGL 在 Web 上的实现。OpenGL 是通过操作 GPU 来完成图形绘制渲染的

## CPU

CPU的工作原理，它就像是一个管道，数据从左侧输入，在CPU中完成处理，然后从右侧输出。
CPU是由多个这样的管道构成的，每个管道我们叫做一个CPU内核，如果你打开你电脑的操作系统，查看本机信息，你可能会看到类似这样的信息：2.6 GHz 六核Intel Core i7，
这里的六核，你可以理解成有6个这样的管道，因此可以同时处理6个任务。CPU的工作能力，与管道本身的处理速度（频率）, 管道的数量（内核数）有关系，
- 频率越高，那么运算处理单一任务的速度就越快
- 内核数越多，那么能同时并行处理的任务数就越多

## GPU
计算机图像是由像素构成，所谓像素，可以简单理解为最终呈现在显示设备上的一个1x1的颜色小方块。
前端的CSS中的px单位，就是像素单位，一张800px长、600px宽的图片，逻辑上是由600*800，也就是48万个像素点构成的。如果要对这张图片的像素进行计算，用CPU来运算的话，单核CPU需要处理48万个微小任务, 所以cpu的架构并不适合图像渲染处理

- GPU的架构
GPU可以看成是由数量非常多的微小管道构成的结构，每一个管道恰好可以处理“一粒沙子”，这样，如果对于一张600像素x800像素的图片，有48万个管道组成的GPU，就可以同时处理这48万个像素点了！事实上，GPU几乎就是这样做的。GPU是并行计算的

数据准备 =》着色处理 =》 帧缓冲 =》 渲染输出
WebGL利用JavaScript来准备数据，将数据通过共享数据结构（ArrayBuffer) 传递给GPU，由GPU进行着色处理，然后再将处理后的数据输出到帧缓冲区，最后再渲染出来。

数据准备一般是通过JavaScript的类型数组（TypedArray）; 着色处理是通过WebGL Program执行一种特殊的glsl语言来实现。在WebGL中，着色阶段通常分成两步，分别是顶点着色和片段着色。