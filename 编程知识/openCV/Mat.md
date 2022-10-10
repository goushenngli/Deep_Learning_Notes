## Mat是什么
 从应用角度来看，可以将Mat理解为一个矩阵，其优点是操作方便，可以使用numpy操作 <br>
## mat属性：
| 字段 | 说明 | 字段 | 说明 |
| :-: | :--| :-: | :-- |
| dims | 维度 | channels | 通道数 |
| rows | 行数 | size | 矩阵大小 |
| cols | 列数 | type | depth+data+channels |
| depth | 像素的位深 | data| 存放数据 |
 其中type字段是其他三个字段的整合，如:CV_8UC3(8代表像素位深、U代表Uint8、C3代表通道数) <br>
## Mat拷贝
### 浅拷贝
浅拷贝只拷贝mat的头部，不拷贝数据，默认情况下为浅拷贝
***赋值就是浅拷贝***
```python
import numpy as np
import cv2
img = cv2.imread('data/0.jpg')
img2 = img
img[10:100, 10:100] = [0, 0, 255]
cv2.imshow('img', img)
cv2.imshow('img2', img2)
cv2.waitKey()
```
### 深拷贝
拷贝mat头部和数据
***使用copy()方法***
```python
import numpy as np
import cv2
img = cv2.imread('data/0.jpg')
img2 = img.copy()
img[10:100, 10:100] = [0, 0, 255]
cv2.imshow('img', img)
cv2.imshow('img2', img2)
cv2.waitKey()
```

## Mat属性(图像的属性)
img.shape

\# 图像占用的空间，高度\*宽度\*2
img.size()

\# 图像每个元素的位深
img.dtype