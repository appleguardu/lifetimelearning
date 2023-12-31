# 光照类型

## 平行光：

平行光的光线是相互平行的，平行光具有方向。平行光可以看做是无限远处的光源发出的光。因为太阳距离地球很远，所以阳光到达地球时可以认为是平行的，平行光的定义很简单，

只需要有`一个方向`和`一个颜色`即可。

漫反射颜色 = 入射光颜色 _ 表面基底色 _ cosθ
rgba 分量相乘

入射角 0 的求法

向量 n _ 向量 m = |n|_|m|\*cos0

归一化的单位向量 n \* m = cos0

cos0 = 光线方向向量 \* 法线方向向量

法向量：以点为基准， 朝向谁看 n ->

## 点光源：

点光源是从一个点向周围所有的方向发出的光。点光源光可以用来表示现实生活中的灯泡、火焰等。我们需要指定点`光源的位置`和`颜色`。
光线的方向将根据点光源的位置和被照射的部位计算出来，因为点光源光在场景内的不同位置是不同的。

** 点光源需要求入射光线向量 **

点光源 =》 各个顶点的方向向量

光线向量 = 顶点向量 - 点光源向量

## 环境光：

是指那些经光源（点光源或平行光）发出后，被墙壁等物体反射多次，然后照到物体表面上的光。

环境光从`各个角度`照射物体，其强度都是相同的。均匀的光照

# 反射类型

## 漫反射是针对平行光和点光源而言的。

漫反射是针对现实生活中大部分粗糙材质（比如塑料、岩石等）而建立的理想反射模型，其反射光在各个方向上是均匀的：

漫反射颜色 = 入射光颜色 _ 表面基底色 _ cosθ

## 环境反射是针对环境光而言的。

在环境反射中，反射光的方向可以认为就是入射光的反方向。由于环境光照射物体的方式是各个方向均匀的、强度相等的，所以反射光的各个方向也是均匀的：

环境反射颜色 = 入射光颜色 _ 表面基底色 _ （cos0 = 1）

# 法线

物体表面的朝向，即垂直与表面的方向，又称法线或法向量。法向量有三个分量，向量 xyz。比如：向量（1,0,0）表示 x 轴的正方向，（0,0,1）表示 z 轴正方向

# 逐顶点光照

光照和颜色逻辑在顶点着色器中进行处理

顶点着色器中 进行线性插值， 每个片元的颜色会存在误差

# 逐片元光照

每个像素被填充到光栅化的颜色，并写入到颜色缓冲区，直接最后一个片元处理完

每个像素都进行计算

计算条件：
- 片元在世界坐标系的坐标
- 片元处的法向量

