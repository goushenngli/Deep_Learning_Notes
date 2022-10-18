
```C++
client = new QTcpSocket(this);
client->connectToHost(QHostAddress("192.168.1.160"), 8001);
while(true){
	//qt发送的数据为字节流，这是json转字节流方法，详情见官方文档
	QByteArray bytearrayJson = documentJson.toJson();
	client->write(bytearrayJson);
	//阻塞状态等待监听信道数据
	client->waitForReadyRead();
	//获取返回数据，官方文档描述输出为字节流，不知道为什么可以用QString接收，隐式转换?
	QString str=client->readAll();
```