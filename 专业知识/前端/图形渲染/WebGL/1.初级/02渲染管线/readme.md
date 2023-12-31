# 渲染管线

渲染管线就像一条流水线，由一系列具有特定功能的数字电路单元组成，下一个功能单元处理上一个功能单元生成的数据，逐级处理数据。

顶点着色器和片元着色器是可编程的功能单元，拥有更大的自主性，还有光栅器、深度测试等不可编程的功能单元。

CPU 会通过 WebGL API 和 GPU 通信，传递着色器程序和数据，GPU 执行的着色器程序可以通过 useProgram 方法切换，

传递数据就是把 CPU 主存中的数据传送到 GPU 的显存中。

## 顶点着色器

顶点着色器是 GPU 渲染管线上一个可以执行着色器语言的功能单元，具体执行的就是顶点着色器程序，WebGL 顶点着色器程序在 Javascript 中以字符串的形式存在，通过编译处理后传递给顶点着色器执行。

顶点着色器主要作用就是 `执行顶点着色器程序对顶点进行变换计算`
比如顶点位置坐标执行进行旋转、平移等矩阵变换，`变换后新的顶点坐标然后赋值给内置变量 gl_Position，作为顶点着色器的输出`，图元装配和光栅化环节的输入。

## 图元装配

顶点变换后的操作是图元装配(primitive assembly)，硬件上具体是怎么回事不用思考，从程序的角度来看，就是 `绘制函数 drawArrays()或 drawElements()第一个参数绘制模式 mode 控制顶点如何装配为图元`

- gl.LINES 的定义的是把两个顶点装配成一个线条图元
- gl.TRIANGLES 定义的是三个顶点装配为一个三角面图元
- gl.POINTS 定义的是一个点域图元。

## 光栅化

将图元光栅化 =》 变成像素单元块 （片元）的过程

## 片元着色器

片元着色器和顶点着色器一样是 GPU 渲染管线上一个可以执行着色器程序的功能单元，
顶点着色器处理的是逐顶点处理顶点数据，片元着色器是逐片元处理片元数据。

通过给内置变量 gl_FragColor 赋值可以给每一个片元进行着色， 值可以是一个确定的 RGBA 值，可以是一个和片元位置相关的值，也可以是插值后的顶点颜色。

除了给片元进行着色之外，通过关键字 discard 还可以实现哪些片元可以被丢弃，被丢弃的片元不会出现在帧缓冲区，自然不会显示在 canvas 画布上。
