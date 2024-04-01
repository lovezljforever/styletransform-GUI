# 这是什么项目？
>用于进行风格迁移的GUI应用程序小项目

# 效果是什么？
>将一个被称为风格图的图像的风格（纹理，色调）迁移到内容图上
>尽量做到“形不变而神变”

# 效果有多强？
>受限于迁移算法的原因，一般

# 如何开始？
>运行gui.py

# 项目架构
```py
gui.py <———————— transfer_ui.py
|
|
run.py————————————————————————————————
^                  ^                ^
|                  |                |
|                  |                |
build.py <———> model.vgg19.py    read_imng.py
```

# 杂七杂八
+ 为什么这个项目明明这么简单却有500+MB？
	VGG19的参数太多了，1.3亿+
	注：这个放在Github的项目使用的是经过裁剪的网络模型（见mini_vgg19相关文件），只有前五层的参数
+ 可以用其他model吗？
	可以，VGG16及以下都可，但是残差网络稠密网络甚至注意力机制参与的网络慎用，会出问题
+ VGG19是自己训练的吗？
	不是，1400w+的数据集，1000分类，没有足够的计算资源
+ 优化算法是LBFGS？
	这算法是二阶优化算法拟牛顿法BFGS的内存受限版本，Adam倒是可以用，收敛速度不太行
	具体来说，BFGS通过某种手段去通过迭代计算无限逼近Hessian矩阵，从而进行牛顿法计算，但是这方法太耗内存了，故提出只有有限步的迭代过程才会对迭代产生的二阶矩阵有影响，由此提出内存受限的拟牛顿法