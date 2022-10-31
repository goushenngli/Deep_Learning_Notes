## 项目文件配置
需要在cmakelist.txt中添加
```CMAKE
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Sql REQUIRED)
target_link_libraries(YouProjectName Qt${QT_VERSION_MAJOR}::Sql)
```
## SQLite
sqlite是以`.DB`文件存储到`build`文件夹下的，不需要通过网络进行连接，帐号和密码可以不设置。具体创建方式可见该文章[Qt使用sqlite](https://blog.csdn.net/qq_37266079/article/details/88345547)
连接测试代码:
```C++
#include <QCoreApplication>
#include <qsqldatabase.h>
#include <QSqlQuery>
#include <QSqlError>
#include <QSqlRecord>
//#include <qmessagebox>
//#include <QLabel>
#include <QTime>
int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);
    qDebug() << QSqlDatabase::drivers();
  
    QSqlDatabase database;
    if (QSqlDatabase::contains("qt_sql_default_connection"))
    {
        database = QSqlDatabase::database("qt_sql_default_connection");
    }
    else
    {
        database = QSqlDatabase::addDatabase("QSQLITE");
        database.setDatabaseName("MyDataBase.db");
    }
  
    if (!database.open())
    {
        qDebug() << "Error: Failed to connect database." << database.lastError();
    }
    else
    {
        qDebug() << "NB!!!!!!!";
        QSqlQuery sqlQuery;
  
        QString str_sql = "";
        str_sql = "create table student (id int primary key,name text ,age int)";
        if(!sqlQuery.exec(str_sql))
        {
            qDebug()<<"创建student表失败！！";
        }
        else
        {
            qDebug()<<"创建student表成功";
        }
    }
    
    return a.exec();
}
```
### 参考资料
[Qt使用sqlite(实际使用)](https://blog.csdn.net/qq_37266079/article/details/88345547)
[CSDN使用ODBC连接数据库](https://blog.csdn.net/m0_38128647/article/details/89482413)



## 数据库链接操作
```C++
    //数据库连接
    if (QSqlDatabase::contains("qt_sql_default_connection"))
    {
        database = QSqlDatabase::database("qt_sql_default_connection");
    }
    else
    {
        database = QSqlDatabase::addDatabase("QSQLITE");
        database.setDatabaseName("MyDataBase.db");
    }
    sqlQuery = QSqlQuery(database);
    qDebug() << "Error: Failed to connect database." <<database.lastError();
    database.open();
```
## 数据库对象使用
```C++
//如果查询结果为空的话则结束
if(!sql_pro.sqlQuery.exec(str_sql)){return;}
//必须在获取数据前执行.next()函数
while(sql_pro.sqlQuery.next()){
	QString pro_name = sql_pro.sqlQuery.value(1).toString();
	QString start_station = sql_pro.sqlQuery.value(2).toString();
	QString end_station = sql_pro.sqlQuery.value(3).toString();
```


## 拼接sql语句
因为在项目查询时候需要获取ui界面控件的内容，然后根据ui控件中的条件拼接sql语句进行查询
### ui控件内容控制
```C++
//获取控件内容：ui->控件名称->text()
QString start = ui->Start_dateEdit->text();
//设置控件内容：ui->控件名称->setText()
ui->Start_dateEdit->setText("内容");
```
[Qt常用UI控件读取、写入方法_进击的小码农a的博客-CSDN博客](https://blog.csdn.net/weixin_41157654/article/details/80820478)

### sql语句拼接--模糊查询
sql支持模糊查询，形式为：
```sql
SELECT * FROM tb_Project WHERE sections_name like '%模糊查询字段%'
```
经过尝试，可以将sql语句写成这种形式：
```sql
 SELECT * FROM tb_Project WHERE sections_name like '%%' AND detector like '%%'
```
当模糊字段为空时，可以理解为条件无效，不会报错
### 字符串拼接
再加上C++中字符串拼接语法("%1"、"%2"这些是占位符)：
```C++
str = QString("%1 was born in %2").arg("John").arg(1988);
```
```C++
QString str_sql = QString("SELECT * FROM tb_Project WHERE sections_name like '%%1%' AND detector like '%%2%'").arg(roadName).arg(detector);
```
