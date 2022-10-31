获取经纬度坐标的程序逻辑是
	每当通道有数据就触发`readyRead()`,QIODevice的方法
	将`readyRead()`和处理函数连接
	每当有数据时就会触发处理函数进行处理

### 出现的问题
处理函数读取到的数据可能并不完整，因为触发是有数据就触发，并没有考虑通道内的数据是否完整
### 解决
QIODevice内部提供canReadLine()方法来判断数据完整性
### 代码
```C++
void CammerWidget::readData()  //读串口数据
{
    QString gngga="GGA";
	//判断数据完整性
    if(_myCom->canReadLine()){
        QByteArray qStr=_myCom->readLine();
        QString str(qStr);
        if(str.contains(gngga)){
            qDebug().noquote()<<qStr<<"--------------";
            N=str.section(',', 2,2);
            E=str.section(',',4,4);
        }
    }
}
```

# 有问题看官方文档
[QIODevice Class #canReadLine()| Qt Core 6.4.0](https://doc.qt.io/qt-6/qiodevice.html#canReadLine)