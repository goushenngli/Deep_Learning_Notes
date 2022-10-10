# 模型加速方法
**模型加速有两种方法比较流行：**
 1. deepstream(主要用于视频)
 2. tensorRT
本次使用的是tensorRT方式对安全帽项目进行加速<br>
## [yolov7](https://github.com/WongKinYiu/yolov7)加速
### 环境搭建
```linux
pip install --upgrade setuptools pip --user 
pip install nvidia-pyindex
pip install onnx_graphsurgeon
pip install onnx>=1.9.0
pip install onnxruntime
pip install --ignore-installed PyYAML
pip install --upgrade nvidia-tensorrt
pip install pycuda
pip install protobuf<4.21.3
pip install onnx-simplifier>=0.3.6 --user
```
清华源：
```linux
pip install --upgrade setuptools pip --user -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install nvidia-pyindex -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install onnx_graphsurgeon -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install onnx>=1.9.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install onnxruntime -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install --ignore-installed PyYAML -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install --upgrade nvidia-tensorrt -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pycuda -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install protobuf<4.21.3 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install onnx-simplifier>=0.3.6 --user -i https://pypi.tuna.tsinghua.edu.cn/simple
```
### pt文件转[[onnx]]
yolov7自带了转onnx格式的python文件，执行以下命令后会生成与pt文件同名的onnx文件
```linux
python3 export.py --weights ./yolov7.pt --grid --simplify --include-nms
```
### onnx文件转trt
这个需要先去下载python版本的tensorrt
```linux
git clone https://github.com/Linaom1214/tensorrt-python.git
```
然后cd到该项目目录下，使用
```linux
python3 export.py -o ./yolov7.onnx -e ./yolov7.trt -p fp16
```
命令进行转换，其中-p参数建议使用fp16,即半精度形式，具体参数用法可见超参数介绍<br>
# `出现的问题
### 使用转化后的trt文件进行预测的时候报错
错误信息：
```python
AttributeError: 'NoneType' object has no attribute 'create_execution_context'
```
原因：原先是在云端转化的，可能是与本地环境相差太大
解决：在本地转化<br>
### trt多线程问题
错误信息：
```python
[TensorRT] ERROR: ../rtSafe/cuda/caskConvolutionRunner.cpp (408) - Cask Error in checkCaskExecError<false>: 11 (Cask Convolution execution)
[TensorRT] ERROR: FAILED_EXECUTION: std::exception
```
解决：参考[trt多线程问题](https://blog.csdn.net/qq_39056987/article/details/116058116)
```python
# 在py文件开头添加如下代码

import pycuda.driver as cuda

cuda.init()
device = cuda.Device(0)
ctx = device.make_context()

# .
# 代码省略
# .

# 在调用执行tensorrt推理函数时上下添加两行

ctx.push()
result = tensorrt_infer(img）  # 我自己的trt推理函数
ctx.pop()
```
<br>
# 参考
[jupyterNotbook示例项目](https://colab.research.google.com/gist/AlexeyAB/fcb47ae544cf284eb24d8ad8e880d45c/yolov7trtlinaom.ipynb#scrollTo=sSDOngglBk_O)