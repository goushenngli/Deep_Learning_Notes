## mAP
 Mean Average Percision(均值平均精度)，一般指的是所有图片内的所有类别的 [[AP]] 的平均值<br>
## mAP@0.5：mean Average Precision（IoU=0.5）
 即将[[IoU]]设为 0.5 时，计算每一类的所有图片的 AP，然后所有类别求平均，即 mAP<br>
 如图所示，AP50，AP60，AP70…… 等等指的是取 detector 的 IoU 阈值大于 0.5，大于 0.6，大于 0.7…… 等等。数值越高，即阈值越大，精度越低。
[![jzEFlq.png](https://s1.ax1x.com/2022/07/26/jzEFlq.png)](https://imgtu.com/i/jzEFlq)
## mAP@.5:.95（mAP@\[.5:.95\]）
表示在不同 IoU 阈值（从 0.5 到 0.95，步长 0.05）
 （0.5、0.55、0.6、0.65、0.7、0.75、0.8、0.85、0.9、0.95）上的平均 mAP。<br>
## 参考
[CSDN原文](https://blog.csdn.net/ruyingcai666666/article/details/109670567)