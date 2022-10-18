# 连接方法
需要在cmakelist.txt中添加
```CMAKE
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Sql REQUIRED)
target_link_libraries(YouProjectName Qt${QT_VERSION_MAJOR}::Sql)
```
## SQLite
sqlite是以`.DB`文件存储到`build`文件夹下的，不需要通过网络进行连接，帐号和密码可以不设置。具体创建方式可见该文章[Qt使用sqlite](https://blog.csdn.net/qq_37266079/article/details/88345547)
==测试代码==:
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
## ODBC
测试代码：
```C++
#include <QSqlDatabase>
QSqlDatabase db = QSqlDatabase::addDatabase("QODBC");
db.setHostName("127.0.0.1");
db.setPort(3306);
db.setDatabaseName("QtODBCmySql");
db.setUserName("root");
db.setPassword("qwer");
bool ok = db.open();
if (ok){
	std::cout<<"NB!!!!!"<<std::endl;
}
else {
	std::cout<<"LJ?????"<<std::endl;
}
return a.exec();
```

> [!tip] qt连接数据库声明
> ![[数据库对象共享#1、头文件调用]]

方法参考[CSDN使用ODBC连接数据库](https://blog.csdn.net/m0_38128647/article/details/89482413)数据库能够连接，但是不能查询，考虑是数据库绑定问题，查了挺多资料，暂未解决[查询数据库解决思路CSDN](https://blog.csdn.net/qq_43680827/article/details/123284388)  
# 参考资料
[Qt使用sqlite(实际使用)](https://blog.csdn.net/qq_37266079/article/details/88345547)
[CSDN使用ODBC连接数据库](https://blog.csdn.net/m0_38128647/article/details/89482413)
