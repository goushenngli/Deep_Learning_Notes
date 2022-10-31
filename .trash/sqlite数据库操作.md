
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

