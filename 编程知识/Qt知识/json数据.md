## QJsonObject
 QJsonObject类用于封装JSON对象，用于对json数据进行操作
```C++
//创建json对象
QJsonObject json;
//对象赋值
json.insert("pic_path",fol_path);
json.insert("txt_path",txt_path);
json.insert("exc_path",exc_path);
```


## QJsonDocument
QJsonDocument提供了读写Json文档的方法。
QJsonDocument是一个包含了完整JSON文档的类，支持以UTF-8编码的文本和QT自身的二进制格式来读写JSON文档。
```C++
//string转json
QJsonDocument jsonDocument = QJsonDocument::fromJson(str.toLocal8Bit().data());
QJsonObject jsonObject = jsonDocument.object();

//json转string
QString txt_path_return= jsonObject.find("txt_path")->toString();
```


## QJsonArray
QJsonArray类用于封装JSON数组。


## json和QString转换
```C++
QJsonObject MainWindow::QstringToJson(QString jsonString)
{
    QJsonDocument jsonDocument = QJsonDocument::fromJson(jsonString.toLocal8Bit().data());
    if(jsonDocument.isNull())
    {
        qDebug()<< "String NULL"<< jsonString.toLocal8Bit().data();
    }
    QJsonObject jsonObject = jsonDocument.object();
    return jsonObject;
}
 
QString MainWindow::JsonToQstring(QJsonObject jsonObject)
{
    return QString(QJsonDocument(jsonObject).toJson());
}
```