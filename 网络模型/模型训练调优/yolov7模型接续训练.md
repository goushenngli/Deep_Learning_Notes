1. 📂在`runs/train`文件夹下将想要接续的模型exp后面的删除或者移动
2. 👉转回`train.py`文件，将超参数`resume`的默认设置为`True`
3. 👍接下来运行`python3 train.py`就会在原有的exp文件夹后面继续训练

# 参考链接

[🌐CSDNyolov7接续训练](https://blog.csdn.net/ShakalakaPHD/article/details/120635894)