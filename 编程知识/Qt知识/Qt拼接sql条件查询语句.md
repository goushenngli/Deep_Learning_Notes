因为在项目查询时候需要获取ui界面控件的内容，然后根据ui控件中的条件拼接sql语句进行查询

# ui控件内容控制
```C++
//获取控件内容：ui->控件名称->text()
QString start = ui->Start_dateEdit->text();
//设置控件内容：ui->控件名称->setText()
ui->Start_dateEdit->setText("内容");
```
[Qt常用UI控件读取、写入方法_进击的小码农a的博客-CSDN博客](https://blog.csdn.net/weixin_41157654/article/details/80820478)

# sql语句拼接
## sql模糊查询
sql支持模糊查询，形式为：
```sql
SELECT * FROM tb_Project WHERE sections_name like '%模糊查询字段%'
```
经过尝试，可以将sql语句写成这种形式：
```sql
 SELECT * FROM tb_Project WHERE sections_name like '%%' AND detector like '%%'
```
当模糊字段为空时，可以理解为条件无效，不会报错

## 字符串拼接
再加上C++中字符串拼接语法("%1"、"%2"这些是占位符)：
```C++
str = QString("%1 was born in %2").arg("John").arg(1988);
```
```C++
QString str_sql = QString("SELECT * FROM tb_Project WHERE sections_name like '%%1%' AND detector like '%%2%'").arg(roadName).arg(detector);
```

## sql数据库操作

 ![[sqlite数据库操作]]