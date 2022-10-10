
	YOLOv1的核心思想就是利用整张图作为网络的输入，直接在输出层回归bounding box的位置和bounding box所属的类别
通过多层卷积生成bbox的位置和置信度
卷积核的值对于模型训练至关重要
[yolov1](https://zhuanlan.zhihu.com/p/364367221)
yolo的模型输出有30维，这30维中，8维是box的坐标，2维是box的置信度，还有20维是类别。其中坐标的x,y用对应网格的偏移量归一化到0-1之间，w,h用图像的width和height归一化到0-1之间。[![jzEk60.png](https://s1.ax1x.com/2022/07/26/jzEk60.png)](https://imgtu.com/i/jzEk60)


# 损失函数

# 缺点
1.  YOLO对相互靠的很近的物体和很小的群体检测效果不好，这是因为一个网格中只预测了两个框，并且只属于一类；
2. 同一类物体出现的新的不常见的长宽比和其他情况时，泛化能力偏弱；
3. 由于损失函数的问题，定位误差是影响检测效果的主要原因。尤其是大小物体的处理上，还有待加强。
# 参考文献
[yolo图文讲解](https://blog.csdn.net/qq_40716944/article/details/114822515#:~:text=YOLOv1%E7%9A%84%E6%A0%B8%E5%BF%83%E6%80%9D%E6%83%B3%EF%BC%9A%20YOLOv1%E7%9A%84%E6%A0%B8%E5%BF%83%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E5%88%A9%E7%94%A8%E6%95%B4%E5%BC%A0%E5%9B%BE%E4%BD%9C%E4%B8%BA%E7%BD%91%E7%BB%9C%E7%9A%84%E8%BE%93%E5%85%A5%EF%BC%8C%E7%9B%B4%E6%8E%A5%E5%9C%A8%E8%BE%93%E5%87%BA%E5%B1%82%E5%9B%9E%E5%BD%92bounding,box%E7%9A%84%E4%BD%8D%E7%BD%AE%E5%92%8Cbounding%20box%E6%89%80%E5%B1%9E%E7%9A%84%E7%B1%BB%E5%88%AB%E3%80%82)

